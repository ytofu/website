# Shield

AWS Shield Advanced DDoS protection using ytofu YAML.

| Resource | Description |
|----------|-------------|
| [Protection](protection.md) | Shield protections |
| [Protection Group](protection-group.md) | Protection groups |

## Quick Example

```yaml
resource:
  aws_shield_protection:
    example:
      name: example
      resource_arn: ${aws_eip.example.arn}
```
