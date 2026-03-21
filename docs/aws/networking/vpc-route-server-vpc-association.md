# Resource: aws_vpc_route_server_vpc_association

Provides a resource for managing association between VPC (Virtual Private Cloud) route server and a VPC.

## Basic Example

```yaml
resource:
  aws_vpc_route_server_vpc_association:
    example:
      route_server_id: ${aws_vpc_route_server.example.route_server_id}
      vpc_id: ${aws_vpc.example.id}
```

## Argument Reference

The following arguments are required:

* `route_server_id` - (Required) The unique identifier for the route server to be associated.
* `vpc_id` - (Required) The ID of the VPC to associate with the route server.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_vpc_route_server_vpc_association.example rs-12345678,vpc-0f001273ec18911b1
```
