# Dataexchange Event Action

Manage Dataexchange Event Action resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dataexchange_event_action:
    example:
      event:
        revision_published:
          data_set_id: ${aws_dataexchange_data_set.example.id}
      action:
        export_revision_to_s3:
          revision_destination:
            bucket: ${aws_s3_bucket.example.bucket}
            key_pattern: "$${Revision.CreatedAt}/$${Asset.Name}"
          encryption:
            type: "aws:kms"
            kms_key_arn: ${aws_kms_key.example.arn}
```
