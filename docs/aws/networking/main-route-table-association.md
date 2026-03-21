# Resource: aws_main_route_table_association

Provides a resource for managing the main routing table of a VPC.

## Basic Example

```yaml
resource:
  aws_main_route_table_association:
    a:
      vpc_id: ${aws_vpc.foo.id}
      route_table_id: ${aws_route_table.bar.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_id` - (Required) The ID of the VPC whose main route table should be set
* `route_table_id` - (Required) The ID of the Route Table to set as the new
  main route table for the target VPC

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the Route Table Association
* `original_route_table_id` - Used internally, see __Notes__ below

## Timeouts

Configuration options:

- `create` - (Default `5m`)
- `update` - (Default `2m`)
- `delete` - (Default `5m`)

[aws-route-tables]: http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Route_Tables.html#Route_Replacing_Main_Table
[tf-route-tables]: /docs/providers/aws/r/route_table.html
[tf-default-route-table]: /docs/providers/aws/r/default_route_table.html
