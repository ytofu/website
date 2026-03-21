# Resource: aws_vpc_route_server_propagation

Provides a resource for managing propagation between VPC (Virtual Private Cloud) route server and a route table.

## Basic Example

```yaml
resource:
  aws_vpc_route_server_propagation:
    example:
      route_server_id: ${aws_vpc_route_server.example.route_server_id}
      route_table_id: ${aws_route_table.example.id}
```

## Argument Reference

The following arguments are required:

* `route_server_id` - (Required) The unique identifier for the route server to be associated.
* `route_table_id` - (Required) The ID of the route table to which route server will propagate routes.

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
ytofu import aws_vpc_route_server_propagation.example rs-12345678,rtb-656c65616e6f72
```
