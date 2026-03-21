# Resource: aws_redshiftserverless_endpoint_access

Creates a new Amazon Redshift Serverless Endpoint Access.

## Basic Example

```yaml
resource:
  aws_redshiftserverless_endpoint_access:
    example:
      endpoint_name: example
      workgroup_name: example
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `endpoint_name` - (Required) The name of the endpoint.
* `owner_account` - (Optional) The owner Amazon Web Services account for the Amazon Redshift Serverless workgroup.
* `subnet_ids` - (Required) An array of VPC subnet IDs to associate with the endpoint.
* `vpc_security_group_ids` - (Optional) An array of security group IDs to associate with the workgroup.
* `workgroup_name` - (Required) The name of the workgroup.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the Redshift Serverless Endpoint Access.
* `id` - The Redshift Endpoint Access Name.
* `address` - The DNS address of the VPC endpoint.
* `port` - The port that Amazon Redshift Serverless listens on.
* `vpc_endpoint` - The VPC endpoint or the Redshift Serverless workgroup. See `VPC Endpoint` below.

#### VPC Endpoint

* `vpc_endpoint_id` - The DNS address of the VPC endpoint.
* `vpc_id` - The port that Amazon Redshift Serverless listens on.
* `network_interface` - The network interfaces of the endpoint.. See `Network Interface` below.

##### Network Interface

* `availability_zone` - The availability Zone.
* `network_interface_id` - The unique identifier of the network interface.
* `private_ip_address` - The IPv4 address of the network interface within the subnet.
* `subnet_id` - The unique identifier of the subnet.

## Import

```bash
ytofu import aws_redshiftserverless_endpoint_access.example example
```
