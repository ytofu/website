# Appstream Image Builder

Manage Appstream Image Builder resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appstream_image_builder:
    test_fleet:
      name: Name
      description: Description of a ImageBuilder
      display_name: Display name of a ImageBuilder
      enable_default_internet_access: false
      image_name: AppStream-WinServer2019-10-05-2022
      instance_type: stream.standard.large
      vpc_config:
        subnet_ids: 
          - ${aws_subnet.example.id}
      tags:
        Name: Example Image Builder
```
