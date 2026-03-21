# Resource: aws_apigatewayv2_vpc_link

Manages an Amazon API Gateway Version 2 VPC Link.

## Basic Example

```yaml
resource:
  aws_apigatewayv2_vpc_link:
    example:
      name: example
      security_group_ids: 
        - ${data.aws_security_group.example.id}
      subnet_ids: ${data.aws_subnets.example.ids}
      tags:
        Usage: example
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name of the VPC Link. Must be between 1 and 128 characters in length.
* `security_group_ids` - (Required) Security group IDs for the VPC Link.
* `subnet_ids` - (Required) Subnet IDs for the VPC Link.
* `tags` - (Optional) Map of tags to assign to the VPC Link. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - VPC Link identifier.
* `arn` - VPC Link ARN.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_apigatewayv2_vpc_link.example aabbccddee
```
