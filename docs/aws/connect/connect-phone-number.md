# Connect Phone Number

Manage Connect Phone Number resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_phone_number:
    example:
      target_arn: ${aws_connect_instance.example.arn}
      country_code: US
      type: DID
      tags: 
```

## Description

```yaml
resource:
  aws_connect_phone_number:
    example:
      target_arn: ${aws_connect_instance.example.arn}
      country_code: US
      type: DID
      description: example description
```

## Prefix to filter phone numbers

```yaml
resource:
  aws_connect_phone_number:
    example:
      target_arn: ${aws_connect_instance.example.arn}
      country_code: US
      type: DID
      prefix: +18005
```
