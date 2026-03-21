# Lambda Layer Version

Manage Lambda Layer Version resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lambda_layer_version:
    example:
      filename: lambda_layer_payload.zip
      layer_name: lambda_layer_name
      compatible_runtimes: 
        - nodejs20.x
```

## Layer with S3 Source

```yaml
resource:
  aws_lambda_layer_version:
    example:
      s3_bucket: ${aws_s3_object.lambda_layer_zip.bucket}
      s3_key: ${aws_s3_object.lambda_layer_zip.key}
      layer_name: lambda_layer_name
      compatible_runtimes: 
        - nodejs20.x
        - python3.12
      compatible_architectures: 
        - x86_64
        - arm64
```

## Layer with Multiple Runtimes and Architectures

```yaml
resource:
  aws_lambda_layer_version:
    example:
      filename: lambda_layer_payload.zip
      layer_name: multi_runtime_layer
      description: Shared utilities for Lambda functions
      license_info: MIT
      source_code_hash: ${filebase64sha256("lambda_layer_payload.zip")}
      compatible_runtimes:
        - nodejs18.x
        - nodejs20.x
        - python3.11
        - python3.12
      compatible_architectures: 
        - x86_64
        - arm64
```
