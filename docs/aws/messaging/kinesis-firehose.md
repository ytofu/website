# Kinesis Firehose Delivery Stream

Create delivery streams for data loading using ytofu YAML.

## S3 Destination

```yaml
resource:
  aws_kinesis_firehose_delivery_stream:
    example:
      name: example-stream
      destination: extended_s3
      extended_s3_configuration:
        role_arn: ${aws_iam_role.firehose.arn}
        bucket_arn: ${aws_s3_bucket.bucket.arn}
        buffering_size: 10
        buffering_interval: 400
        compression_format: GZIP
```

## OpenSearch Destination

```yaml
resource:
  aws_kinesis_firehose_delivery_stream:
    example:
      name: example-opensearch
      destination: opensearch
      opensearch_configuration:
        domain_arn: ${aws_opensearch_domain.example.arn}
        role_arn: ${aws_iam_role.firehose.arn}
        index_name: example
        type_name: _doc
        s3_configuration:
          role_arn: ${aws_iam_role.firehose.arn}
          bucket_arn: ${aws_s3_bucket.bucket.arn}
```

## With Data Transformation

```yaml
resource:
  aws_kinesis_firehose_delivery_stream:
    example:
      name: example-transformed
      destination: extended_s3
      extended_s3_configuration:
        role_arn: ${aws_iam_role.firehose.arn}
        bucket_arn: ${aws_s3_bucket.bucket.arn}
        processing_configuration:
          enabled: true
          processors:
            - type: Lambda
              parameters:
                - parameter_name: LambdaArn
                  parameter_value: ${aws_lambda_function.processor.arn}:$LATEST
```
