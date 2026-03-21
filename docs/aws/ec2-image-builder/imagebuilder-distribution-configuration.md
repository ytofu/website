# Imagebuilder Distribution Configuration

Manage Imagebuilder Distribution Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_imagebuilder_distribution_configuration:
    example:
      name: example
      distribution:
        ami_distribution_configuration:
          ami_tags:
            CostCenter: IT
          name: "example-{{ imagebuilder:buildDate }}"
          launch_permission:
            user_ids: 
              - 123456789012
        launch_template_configuration:
          launch_template_id: lt-0aaa1bcde2ff3456
        region: us-east-1
```
