# S3 Access Point

Manage S3 Access Point resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_s3_access_point:
    example:
      bucket: ${aws_s3_bucket.example.id}
      name: example
```

## S3 on Outposts Bucket

```yaml
resource:
  aws_s3control_bucket:
    example:
      bucket: example

resource:
  aws_s3_access_point:
    example:
      bucket: ${aws_s3control_bucket.example.arn}
      name: example
      vpc_configuration:
        vpc_id: ${aws_vpc.example.id}

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16
```

## AWS Partition Directory Bucket

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
      bucket: ${aws_s3_directory_bucket.test.bucket}
      name: example--zoneId--xa-s3
```
