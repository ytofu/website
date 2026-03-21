# Resource: aws_s3control_directory_bucket_access_point_scope

Provides a resource to manage the access point scope for a directory bucket.

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

## Argument Reference

This resource supports the following arguments:

* `account_id` - (Required) The AWS account ID that owns the specified access point.
* `name` - (Required) The name of the access point that you want to apply the scope to.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `scope` - (Optional). Scope is used to restrict access to specific prefixes, API operations, or a combination of both. To remove the `scope`, set it to `{permissions=[] prefixes=[]}`. The default scope is `{permissions=[] prefixes=[]}`.

### Scope Configuration block

The following arguments are optional:

* `permissions` – (Optional) You can specify a list of API operations as permissions for the access point.
* `prefixes` – (Optional) You can specify a list of prefixes, but the total length of characters of all prefixes must be less than 256 bytes.

* For more information on access point scope, see [AWS Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-points-directory-buckets-manage-scope.html).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

## Import

```bash
ytofu import aws_s3control_directory_bucket_access_point_scope.example example--zoneid--xa-s3,123456789012
```
