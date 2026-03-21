# Redshiftserverless Custom Domain Association

Manage Redshiftserverless Custom Domain Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_acm_certificate:
    example:
      domain_name: example.com

resource:
  aws_redshiftserverless_namespace:
    example:
      namespace_name: example-namespace

resource:
  aws_redshiftserverless_workgroup:
    example:
      workgroup_name: example-workgroup
      namespace_name: ${aws_redshiftserverless_namespace.example.namespace_name}

resource:
  aws_redshiftserverless_custom_domain_association:
    example:
      workgroup_name: ${aws_redshiftserverless_workgroup.example.workgroup_name}
      custom_domain_name: example.com
      custom_domain_certificate_arn: ${aws_acm_certificate.example.arn}
```
