# ytofu

**OpenTofu fork with first-class YAML support**

ytofu brings the Configuration as Data paradigm to Terraform, allowing you to define your infrastructure using YAML instead of HCL.

## Why ytofu?

- **YAML-native**: Write infrastructure code in YAML, a format you already know
- **Configuration as Data**: Treat your infrastructure definitions as pure data
- **OpenTofu compatible**: Built on OpenTofu, fully compatible with existing providers
- **Simplified workflows**: Easier integration with GitOps and Kubernetes-style tooling

## Configuration as Data

ytofu embraces the **Configuration as Data** philosophy. Your infrastructure is defined as plain YAML data, not code:

| Traditional HCL | ytofu YAML |
|-----------------|------------|
| Variables, locals | Concrete values |
| For loops, count | Explicit resources |
| Conditionals | No conditionals |
| Functions | No functions |
| Dynamic blocks | Static definitions |

This means your configurations are:
- **Readable** - Pure data, no logic to trace
- **Auditable** - Easy to review and diff
- **Generatable** - Simple to produce from external tools
- **GitOps-ready** - Works naturally with Kubernetes-style workflows

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
