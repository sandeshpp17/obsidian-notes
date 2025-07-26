A Pulumi Provider allows you to define new resource types, enabling integration with virtually any service or tool. Pulumi providers are ideal when you need to manage resources that are not yet supported by existing Pulumi providers or when you require custom behavior for managing external systems or APIs. Providers are a powerful extension point, but before building a full provider consider if your use case can be covered by [building a component](https://www.pulumi.com/docs/iac/using-pulumi/extending-pulumi/build-a-component/) or using [dynamic provider functions](https://www.pulumi.com/docs/iac/concepts/resources/dynamic-providers/).

### The provider interface[](https://www.pulumi.com/docs/iac/extending-pulumi/build-a-provider/#the-provider-interface)

The Pulumi [Provider](https://pkg.go.dev/github.com/pulumi/pulumi-go-provider#Provider) interface implements the following core methods which form the foundation of Pulumi’s resource lifecycle management:

- **Create** – provisions a new resource
- **Read** – fetches the resource
- **Update** – updates an existing resource
- **Delete** – removes a resource
- **Diff** – computes the differences between the current resource and desired updates to the resource
- **Check** – validates the input parameters
- **Configure** – initializes provider-wide settings (e.g. credentials)