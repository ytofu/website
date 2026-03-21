# Transfer Agreement

Manage Transfer Agreement resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_transfer_agreement:
    example:
      access_role: ${aws_iam_role.test.arn}
      base_directory: /DOC-EXAMPLE-BUCKET/home/mydirectory
      description: example
      local_profile_id: ${aws_transfer_profile.local.profile_id}
      partner_profile_id: ${aws_transfer_profile.partner.profile_id}
      server_id: ${aws_transfer_server.test.id}
```
