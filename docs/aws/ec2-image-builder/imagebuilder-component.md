# Imagebuilder Component

Manage Imagebuilder Component resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_imagebuilder_component:
    example:
      data: '# yamlencode content'
      name: example
      platform: Linux
      version: 1.0.0
```

## URI Document

```yaml
resource:
  aws_imagebuilder_component:
    example:
      name: example
      platform: Linux
      uri: "s3://${aws_s3_object.example.bucket}/${aws_s3_object.example.key}"
      version: 1.0.0
```
