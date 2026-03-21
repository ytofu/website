# Resource: aws_shield_drt_access_log_bucket_association

ytofu resource for managing an AWS Shield DRT Access Log Bucket Association.
Up to 10 log buckets can be associated for DRT Access sharing with the Shield Response Team (SRT).

## Basic Example

```yaml
resource:
  aws_shield_drt_access_role_arn_association:
    test:
      role_arn: "arn:aws:iam:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:example-shield_drt_access_role_name"

resource:
  aws_shield_drt_access_log_bucket_association:
    test:
      log_bucket: example-shield_drt_access_log_bucket
      role_arn_association_id: ${aws_shield_drt_access_role_arn_association.test.id}
```

## Argument Reference

The following arguments are required:

* `log_bucket` - (Required) The Amazon S3 bucket that contains the logs that you want to share.
* `role_arn_association_id` - (Required) The ID of the Role Arn association used for allowing Shield DRT Access.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_shield_drt_access_log_bucket_association.example example-bucket
```
