# Resource: aws_opensearchserverless_vpc_endpoint

ytofu resource for managing an AWS OpenSearchServerless VPC Endpoint.

## Basic Example

```yaml
resource:
  aws_opensearchserverless_vpc_endpoint:
    example:
      name: myendpoint
      subnet_ids: 
        - ${aws_subnet.example.id}
      vpc_id: ${aws_vpc.example.id}
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the interface endpoint.
* `subnet_ids` - (Required) One or more subnet IDs from which you'll access OpenSearch Serverless. Up to 6 subnets can be provided.
* `vpc_id` - (Required) ID of the VPC from which you'll access OpenSearch Serverless.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `security_group_ids` - (Optional) One or more security groups that define the ports, protocols, and sources for inbound traffic that you are authorizing into your endpoint. Up to 5 security groups can be provided.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Unique identified of the Vpc Endpoint.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_opensearchserverless_vpc_endpoint.example vpce-8012925589
```
