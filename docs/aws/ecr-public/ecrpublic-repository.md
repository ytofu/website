# Ecrpublic Repository

Manage Ecrpublic Repository resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecrpublic_repository:
    foo:
      repository_name: bar
      catalog_data:
        about_text: About Text
        architectures: 
          - ARM
        description: Description
        logo_image_blob: ${filebase64(image.png)}
        operating_systems: 
          - Linux
        usage_text: Usage Text
      tags:
        env: production
```
