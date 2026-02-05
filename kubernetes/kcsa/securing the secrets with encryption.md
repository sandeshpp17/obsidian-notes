there are many methods to secure secrets with the KES/KMS key management system and the internal provided by etcd itself.

By default, the API server stores plain-text representations of resources into etcd, with no at-rest encryption.

The `kube-apiserver` process accepts an argument `--encryption-provider-config` that specifies a path to a configuration file. The contents of that file, if you specify one, control how Kubernetes API data is encrypted in etcd. If you are running the kube-apiserver without the `--encryption-provider-config` command line argument, you do not have encryption at rest enabled. If you are running the kube-apiserver with the `--encryption-provider-config` command line argument, and the file that it references specifies the `identity` provider as the first encryption provider in the list, then you do not have at-rest encryption enabled (**the default `identity` provider does not provide any confidentiality protection.**)

If you are running the kube-apiserver with the `--encryption-provider-config` command line argument, and the file that it references specifies a provider other than `identity` as the first encryption provider in the list, then you already have at-rest encryption enabled. However, that check does not tell you whether a previous migration to encrypted storage has succeeded. If you are not sure, see [ensure all relevant data are encrypted](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/#ensure-all-secrets-are-encrypted).

## Understanding the encryption at rest configuration

```yaml
---
#
# CAUTION: this is an example configuration.
#          Do not use this for your own cluster!
#
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
  - resources:
      - secrets
      - configmaps
      - pandas.awesome.bears.example # a custom resource API
    providers:
      # This configuration does not provide data confidentiality. The first
      # configured provider is specifying the "identity" mechanism, which
      # stores resources as plain text.
      #
      - identity: {} # plain text, in other words NO encryption
      - aesgcm:
          keys:
            - name: key1
              secret: c2VjcmV0IGlzIHNlY3VyZQ==
            - name: key2
              secret: dGhpcyBpcyBwYXNzd29yZA==
      - aescbc:
          keys:
            - name: key1
              secret: c2VjcmV0IGlzIHNlY3VyZQ==
            - name: key2
              secret: dGhpcyBpcyBwYXNzd29yZA==
      - secretbox:
          keys:
            - name: key1
              secret: YWJjZGVmZ2hpamtsbW5vcHFyc3R1dnd4eXoxMjM0NTY=
  - resources:
      - events
    providers:
      - identity: {} # do not encrypt Events even though *.* is specified below
  - resources:
      - '*.apps' # wildcard match requires Kubernetes 1.27 or later
    providers:
      - aescbc:
          keys:
          - name: key2
            secret: c2VjcmV0IGlzIHNlY3VyZSwgb3IgaXMgaXQ/Cg==
  - resources:
      - '*.*' # wildcard match requires Kubernetes 1.27 or later
    providers:
      - aescbc:
          keys:
          - name: key3
```

### [Available providers](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/#providers)

Before you configure encryption-at-rest for data in your cluster's Kubernetes API, you need to select which provider(s) you will use.

The following table describes each available provider.

| Name                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Encryption                                                                   | Strength                             | Speed                              | Key length         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ------------------------------------ | ---------------------------------- | ------------------ |
| identity                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | **None**                                                                     | N/A                                  | N/A                                | N/A                |
| Resources written as-is without encryption. When set as the first provider, the resource will be decrypted as new values are written. Existing encrypted resources are **not** automatically overwritten with the plaintext data. The identity provider is the default if you do not specify otherwise.                                                                                                                                                                                                                                                               |                                                                              |                                      |                                    |                    |
| aescbc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | AES-CBC with [PKCS#7](https://datatracker.ietf.org/doc/html/rfc2315) padding | Weak                                 | Fast                               | 16, 24, or 32-byte |
| Not recommended due to CBC's vulnerability to padding oracle attacks. Key material accessible from control plane host.                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                              |                                      |                                    |                    |
| aesgcm                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | AES-GCM with random nonce                                                    | Must be rotated every 200,000 writes | Fastest                            | 16, 24, or 32-byte |
| Not recommended for use except when an automated key rotation scheme is implemented. Key material accessible from control plane host.                                                                                                                                                                                                                                                                                                                                                                                                                                 |                                                                              |                                      |                                    |                    |
| kms v1 _(deprecated since Kubernetes v1.28)_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Uses envelope encryption scheme with DEK per resource.                       | Strongest                            | Slow (_compared to kms version 2_) | 32-bytes           |
| Data is encrypted by data encryption keys (DEKs) using AES-GCM; DEKs are encrypted by key encryption keys (KEKs) according to configuration in Key Management Service (KMS). Simple key rotation, with a new DEK generated for each encryption, and KEK rotation controlled by the user.  <br>Read how to [configure the KMS V1 provider](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider#configuring-the-kms-provider-kms-v1).                                                                                                                      |                                                                              |                                      |                                    |                    |
| kms v2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Uses envelope encryption scheme with DEK per API server.                     | Strongest                            | Fast                               | 32-bytes           |
| Data is encrypted by data encryption keys (DEKs) using AES-GCM; DEKs are encrypted by key encryption keys (KEKs) according to configuration in Key Management Service (KMS). Kubernetes generates a new DEK per encryption from a secret seed. The seed is rotated whenever the KEK is rotated.  <br>A good choice if using a third party tool for key management. Available as stable from Kubernetes v1.29.  <br>Read how to [configure the KMS V2 provider](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider#configuring-the-kms-provider-kms-v2). |                                                                              |                                      |                                    |                    |
| secretbox                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | XSalsa20 and Poly1305                                                        | Strong                               | Faster                             | 32-byte            |
| Uses relatively new encryption technologies that may not be considered acceptable in environments that require high levels of review. Key material accessible from control plane host.                                                                                                                                                                                                                                                                                                                                                                                |                                                                              |                                      |                                    |                    |

The `identity` provider is the default if you do not specify otherwise. **The `identity` provider does not encrypt stored data and provides _no_ additional confidentiality protection.**