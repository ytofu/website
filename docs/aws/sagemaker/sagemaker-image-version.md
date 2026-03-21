# Sagemaker Image Version

Manage Sagemaker Image Version resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_image_version:
    example:
      image_name: ${aws_sagemaker_image.test.id}
      base_image: "012345678912.dkr.ecr.us-west-2.amazonaws.com/image:latest"
```

## With Aliases

```yaml
resource:
  aws_sagemaker_image_version:
    test:
      image_name: ${aws_sagemaker_image.test.id}
      base_image: "012345678912.dkr.ecr.us-west-2.amazonaws.com/image:latest"
      aliases: 
        - latest
        - stable
```
