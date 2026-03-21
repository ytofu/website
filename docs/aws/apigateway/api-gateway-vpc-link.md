# Resource: aws_api_gateway_vpc_link

Provides an API Gateway VPC Link.

## Basic Example

```yaml
resource:
  aws_lb:
    example:
      name: example
      internal: true
      load_balancer_type: network
      subnet_mapping:
        subnet_id: 12345

  aws_api_gateway_vpc_link:
    example:
      name: example
      description: example description
      target_arns: 
        - ${aws_lb.example.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name used to label and identify the VPC link.
* `description` - (Optional) Description of the VPC link.
* `target_arns` - (Required, ForceNew) List of network load balancer arns in the VPC targeted by the VPC link. Currently AWS only supports 1 target.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Identifier of the VpcLink.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_api_gateway_vpc_link.example 12345abcde
```
