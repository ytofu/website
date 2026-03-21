# S3control Directory Bucket Access Point Scope

Manage S3control Directory Bucket Access Point Scope resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_availability_zones:
    available:
      state: available

resource:
  aws_s3_directory_bucket:
    example:
      bucket: example--zoneId--x-s3
      location:
        name: ${data.aws_availability_zones.available.zone_ids[0]}

resource:
  aws_s3_access_point:
    example:
      bucket: ${aws_s3_directory_bucket.example.id}
      name: example--zoneId--xa-s3

resource:
  aws_s3control_directory_bucket_access_point_scope:
    example:
      name: example--zoneId--xa-s3
      account_id: 123456789012
      scope:
        permissions: 
          - GetObject
          - ListBucket
        prefixes: 
          - myobject1.csv
          - "myobject2*"
```
