# Appflow Flow

Manage Appflow Flow resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example_source:
      bucket: example-source

data:
  aws_iam_policy_document:
    example_source:
      statement:
        sid: AllowAppFlowSourceActions
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - appflow.amazonaws.com
        actions:
          - "s3:ListBucket"
          - "s3:GetObject"
        resources:
          - "arn:aws:s3:::example-source"
          - "arn:aws:s3:::example-source/*"

resource:
  aws_s3_bucket_policy:
    example_source:
      bucket: ${aws_s3_bucket.example_source.id}
      policy: ${data.aws_iam_policy_document.example_source.json}

resource:
  aws_s3_object:
    example:
      bucket: ${aws_s3_bucket.example_source.id}
      key: example_source.csv
      source: example_source.csv

resource:
  aws_s3_bucket:
    example_destination:
      bucket: example-destination

data:
  aws_iam_policy_document:
    example_destination:
      statement:
        sid: AllowAppFlowDestinationActions
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - appflow.amazonaws.com
        actions:
          - "s3:PutObject"
          - "s3:AbortMultipartUpload"
          - "s3:ListMultipartUploadParts"
          - "s3:ListBucketMultipartUploads"
          - "s3:GetBucketAcl"
          - "s3:PutObjectAcl"
        resources:
          - "arn:aws:s3:::example-destination"
          - "arn:aws:s3:::example-destination/*"

resource:
  aws_s3_bucket_policy:
    example_destination:
      bucket: ${aws_s3_bucket.example_destination.id}
      policy: ${data.aws_iam_policy_document.example_destination.json}

resource:
  aws_appflow_flow:
    example:
      name: example
      source_flow_config:
        connector_type: S3
        source_connector_properties:
          s3:
            bucket_name: ${aws_s3_bucket_policy.example_source.bucket}
            bucket_prefix: example
      destination_flow_config:
        connector_type: S3
        destination_connector_properties:
          s3:
            bucket_name: ${aws_s3_bucket_policy.example_destination.bucket}
            s3_output_format_config:
              prefix_config:
                prefix_type: PATH
      task:
        source_fields: 
          - exampleField
        destination_field: exampleField
        task_type: Map
        connector_operator:
          s3: NO_OP
      trigger_config:
        trigger_type: OnDemand
```
