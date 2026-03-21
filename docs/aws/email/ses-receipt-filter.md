# SES Receipt Filter

Manage SES Receipt Filter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ses_receipt_filter:
    filter:
      name: block-spammer
      cidr: 10.10.10.10
      policy: Block
```
