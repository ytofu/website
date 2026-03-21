# Resource: aws_datasync_agent

Manages an AWS DataSync Agent deployed on premises.

## Basic Example

```yaml
resource:
  aws_datasync_agent:
    example:
      ip_address: 1.2.3.4
      name: example
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name of the DataSync Agent.
* `activation_key` - (Optional) DataSync Agent activation key during resource creation. Conflicts with `ip_address`. If an `ip_address` is provided instead, ytofu will retrieve the `activation_key` as part of the resource creation.
* `ip_address` - (Optional) DataSync Agent IP address to retrieve activation key during resource creation. Conflicts with `activation_key`. DataSync Agent must be accessible on port 80 from where ytofu is running.
* `private_link_endpoint` - (Optional) The IP address of the VPC endpoint the agent should connect to when retrieving an activation key during resource creation. Conflicts with `activation_key`.
* `security_group_arns` - (Optional) The ARNs of the security groups used to protect your data transfer task subnets.
* `subnet_arns` - (Optional) The Amazon Resource Names (ARNs) of the subnets in which DataSync will create elastic network interfaces for each data transfer task.
* `tags` - (Optional) Key-value pairs of resource tags to assign to the DataSync Agent. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `vpc_endpoint_id` - (Optional) The ID of the VPC (virtual private cloud) endpoint that the agent has access to.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Amazon Resource Name (ARN) of the DataSync Agent.
* `arn` - Amazon Resource Name (ARN) of the DataSync Agent.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `10m`)

## Import

```bash
ytofu import aws_datasync_agent.example arn:aws:datasync:us-east-1:123456789012:agent/agent-12345678901234567
```
