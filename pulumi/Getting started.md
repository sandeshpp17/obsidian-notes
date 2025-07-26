
Pulumi is a IAC (infrastructure as a code) like terraform and open-tofu.

**Why to use pulumi over terraform

**Language support:
- **Terraform:** Uses HashiCorp Configuration Language (HCL), a domain-specific language (DSL) designed specifically for infrastructure provisioning. It also supports JSON.
- **Pulumi:** Supports general-purpose programming languages like Python, TypeScript, JavaScript, Go, C#, and Java, allowing developers to leverage familiar language features and existing toolchains.

**Secrets Management:**
- **Pulumi:** Encrypts secrets during transmission and storage by default.
- **Terraform:** Stores secrets in plain text within the `tfstate` file unless a secure state backend is configured. 

in general way, pulumi provides us the flexibility to build our own dynamic provider which are more flexible than terraform custom plugin provider. 

