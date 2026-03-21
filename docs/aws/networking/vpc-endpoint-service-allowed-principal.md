# Resource: aws_vpc_endpoint_service_allowed_principal

Provides a resource to allow a principal to discover a VPC endpoint service.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_vpc_endpoint_service_allowed_principal:
    allow_me_to_foo:
      vpc_endpoint_service_id: ${aws_vpc_endpoint_service.foo.id}
      principal_arn: ${data.aws_caller_identity.current.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_endpoint_service_id` - (Required) The ID of the VPC endpoint service to allow permission.
* `principal_arn` - (Required) The ARN of the principal to allow permissions.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the association.
