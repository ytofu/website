# Resource: aws_vpclattice_access_log_subscription

ytofu resource for managing an AWS VPC Lattice Service Network or Service Access log subscription.

## Basic Example

```yaml
resource:
  aws_vpclattice_access_log_subscription:
    example:
      resource_identifier: ${aws_vpclattice_service_network.example.id}
      destination_arn: ${aws_s3.bucket.arn}
```

## Argument Reference

The following arguments are required:

* `destination_arn` - (Required, Forces new resource) Amazon Resource Name (ARN) of the log destination.
* `resource_identifier` - (Required, Forces new resource) The ID or Amazon Resource Identifier (ARN) of the service network or service. You must use the ARN if the resources specified in the operation are in different accounts.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `service_network_log_type` - (Optional, Forces new resource) Type of log that monitors your Amazon VPC Lattice service networks. Valid values are: `SERVICE`, `RESOURCE`. Defaults to `SERVICE`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the access log subscription.
* `arn` - Amazon Resource Name (ARN) of the access log subscription.
* `resource_arn` - Amazon Resource Name (ARN) of the service network or service.

## Import

```bash
ytofu import aws_vpclattice_access_log_subscription.example rft-8012925589
```
