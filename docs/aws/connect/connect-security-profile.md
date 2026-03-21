# Connect Security Profile

Manage Connect Security Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_security_profile:
    example:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: example
      description: example description
      permissions:
        - BasicAgentAccess
        - OutboundCallAccess
      tags: 
```
