# EC2 Allowed Images Settings

Manage EC2 Allowed Images Settings resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_allowed_images_settings:
    example:
      state: enabled
      image_criterion:
        image_providers: 
          - amazon
```

## Enable audit mode with specific account IDs

```yaml
resource:
  aws_ec2_allowed_images_settings:
    example:
      state: audit-mode
      image_criterion:
        image_providers: 
          - amazon
          - 123456789012
```
