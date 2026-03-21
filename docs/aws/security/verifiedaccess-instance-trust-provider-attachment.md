# Verifiedaccess Instance Trust Provider Attachment

Manage Verifiedaccess Instance Trust Provider Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_verifiedaccess_instance:
    example:

resource:
  aws_verifiedaccess_trust_provider:
    example:
      device_trust_provider_type: jamf
      policy_reference_name: example
      trust_provider_type: device
      device_options:
        tenant_id: example

resource:
  aws_verifiedaccess_instance_trust_provider_attachment:
    example:
      verifiedaccess_instance_id: ${aws_verifiedaccess_instance.example.id}
      verifiedaccess_trust_provider_id: ${aws_verifiedaccess_trust_provider.example.id}
```
