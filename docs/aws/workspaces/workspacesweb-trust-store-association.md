# Workspacesweb Trust Store Association

Manage Workspacesweb Trust Store Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

resource:
  aws_workspacesweb_trust_store:
    example:
      certificate_list: 
        - example-value

resource:
  aws_workspacesweb_trust_store_association:
    example:
      trust_store_arn: ${aws_workspacesweb_trust_store.example.trust_store_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}
```
