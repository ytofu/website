# ytofu

**OpenTofu fork with first-class YAML support**

ytofu brings the Configuration as Data paradigm to Terraform, allowing you to define your infrastructure using YAML instead of HCL.

## Why ytofu?

- **YAML-native**: Write infrastructure code in YAML, a format you already know
- **Configuration as Data**: Treat your infrastructure definitions as pure data
- **OpenTofu compatible**: Built on OpenTofu, fully compatible with existing providers
- **Simplified workflows**: Easier integration with GitOps and Kubernetes-style tooling

## Quick Example

```yaml
resource:
  aws_instance:
    web:
      ami: ami-0c55b159cbfafe1f0
      instance_type: t2.micro
      tags:
        Name: HelloWorld
```

## Getting Started

Ready to try ytofu? Check out the [Getting Started](getting-started.md) guide.
