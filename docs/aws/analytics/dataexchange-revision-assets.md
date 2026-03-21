# Dataexchange Revision Assets

Manage Dataexchange Revision Assets resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dataexchange_revision_assets:
    example:
      data_set_id: example-data-set-id
      asset:
        create_s3_data_access_from_s3_bucket:
          asset_source:
            bucket: example-bucket
      tags:
        Environment: Production
```
