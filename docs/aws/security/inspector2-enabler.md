# Inspector2 Enabler

Manage Inspector2 Enabler resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_inspector2_enabler:
    example:
      account_ids: 
        - 123456789012
      resource_types: 
        - EC2
```

## For the Calling Account

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_inspector2_enabler:
    test:
      account_ids: 
        - ${data.aws_caller_identity.current.account_id}
      resource_types: 
        - ECR
        - EC2
```
