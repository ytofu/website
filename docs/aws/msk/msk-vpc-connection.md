# Resource: aws_msk_vpc_connection

ytofu resource for managing an AWS Managed Streaming for Kafka VPC Connection.

## Basic Example

```yaml
resource:
  aws_msk_vpc_connection:
    test:
      authentication: SASL_IAM
      target_cluster_arn: aws_msk_cluster.arn
      vpc_id: ${aws_vpc.test.id}
      client_subnets: ${aws_subnet.test[*].id}
      security_groups: 
        - ${aws_security_group.test.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `authentication` - (Required) The authentication type for the client VPC connection. Specify one of these auth type strings: SASL_IAM, SASL_SCRAM, or TLS.
* `client_subnets` - (Required) The list of subnets in the client VPC to connect to.
* `security_groups` - (Required) The security groups to attach to the ENIs for the broker nodes.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `target_cluster_arn` - (Required) The Amazon Resource Name (ARN) of the cluster.
* `vpc_id` - (Required) The VPC ID of the remote client.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the VPC connection.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `60m`)
* `update` - (Default `180m`)
* `delete` - (Default `90m`)

## Import

```bash
ytofu import aws_msk_vpc_connection.example arn:aws:kafka:eu-west-2:123456789012:vpc-connection/123456789012/example/38173259-79cd-4ee8-87f3-682ea6023f48-2
```
