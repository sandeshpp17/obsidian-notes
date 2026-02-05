In kubernetes the pod are ephemeral in nature. To avoid the dataloss we use pv and pvc to store data in node or remote disk.

when the data is stored on the disk. its very important to keep it secure. if the cluster is provisioned use any csp like aws,azure and gcp they provide default disk encryption.

### Securing storage using storageclass.

when storage class are used to provision the persistent volume and persistent volume claim we need to configure the storageclass for securing the data by encrypting it on the remote disk. 

below is the snippet for enabling the disk encryption.

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: ebs-sc
provisioner: ebs.csi.aws.com
parameters:
  csi.storage.k8s.io/fstype: xfs
  type: io1
  encrypted: "true"
```