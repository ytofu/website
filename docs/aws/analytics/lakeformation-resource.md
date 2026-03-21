# Resource: aws_lakeformation_resource

Registers a Lake Formation resource (e.g., S3 bucket) as managed by the Data Catalog. In other words, the S3 path is added to the data lake.

## Basic Example

```yaml
data:
  aws_s3_bucket:
    example:
      bucket: an-example-bucket

resource:
  aws_lakeformation_resource:
    example:
      arn: ${data.aws_s3_bucket.example.arn}
```

## Argument Reference

The following arguments are required:

* `arn` - (Required) Amazon Resource Name (ARN) of the resource.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `role_arn` - (Optional) Role that has read/write access to the resource.
* `use_service_linked_role` - (Optional) Designates an AWS Identity and Access Management (IAM) service-linked role by registering this role with the Data Catalog.
* `hybrid_access_enabled` - (Optional) Flag to enable AWS LakeFormation hybrid access permission mode.
* `with_federation`- (Optional) Whether or not the resource is a federated resource. Set to true when registering AWS Glue connections for federated catalog functionality.
* `with_privileged_access` - (Optional) Boolean to grant the calling principal the permissions to perform all supported Lake Formation operations on the registered data location.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `last_modified` - Date and time the resource was last modified in [RFC 3339 format](https://tools.ietf.org/html/rfc3339#section-5.8).
