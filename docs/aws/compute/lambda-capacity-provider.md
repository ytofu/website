# Resource: aws_lambda_capacity_provider

Manages an AWS Lambda Capacity Provider.

## Basic Example

```yaml
resource:
  aws_lambda_capacity_provider:
    example:
      name: example
      vpc_config:
        subnet_ids: ${aws_subnet.example[*].id}
        security_group_ids: 
          - ${aws_security_group.example.id}
      permissions_config:
        capacity_provider_operator_role_arn: ${aws_iam_role.example.arn}
```

## Manual Scaling with Specific Instance Types

```yaml
resource:
  aws_lambda_capacity_provider:
    example:
      name: example
      vpc_config:
        subnet_ids: ${aws_subnet.example[*].id}
        security_group_ids: 
          - ${aws_security_group.example.id}
      permissions_config:
        capacity_provider_operator_role_arn: ${aws_iam_role.example.arn}
      instance_requirements:
        architectures: 
          - x86_64
        allowed_instance_types: 
          - c6i.2xlarge
          - c7i.2xlarge
      capacity_provider_scaling_config:
        scaling_mode: Manual
        scaling_policies:
          - predefined_metric_type: LambdaCapacityProviderAverageCPUUtilization
```

## Argument Reference

The following arguments are required:

* `name` - (Required) The name of the Capacity Provider.
* `vpc_config` - (Required) Configuration block for VPC settings. See [VPC Config](#vpc_config) below.
* `permissions_config` - (Required) Configuration block for permissions settings. See [Permissions Config](#permissions_config) below.

The following arguments are optional:

* `capacity_provider_scaling_config` - (Optional) Configuration block for scaling policy settings. See [Capacity Provider Scaling Config](#capacity_provider_scaling_config) below.
* `instance_requirements` - (Optional) Configuration block for instance requirements settings. See [Instance Requirements](#instance_requirements) below.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Map of tags assigned to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### vpc_config

* `subnet_ids` - (Required) List of subnet IDs for the VPC.
* `security_group_ids` - (Required) List of security group IDs for the VPC.

### permissions_config

* `capacity_provider_operator_role_arn` - (Required) The ARN of the IAM role that allows Lambda to manage the Capacity Provider.

### capacity_provider_scaling_config

* `max_vcpu_count` - (Optional) The maximum number of VCPUs for the Capacity Provider.
* `scaling_mode` - (Required) The scaling mode for the Capacity Provider. Valid values are `"Auto"` and `"Manual"`. Defaults to `"Auto"`.
* `scaling_policies` - (Optional) List of scaling policies. Only required if `scaling_mode` is set to `"Manual"`. See [Scaling Policies](#scaling_policies) below.

#### scaling_policies

* `predefined_metric_type` - (Required) The predefined metric type for the scaling policy. Valid values are `"LambdaCapacityProviderAverageCPUUtilization"`.
* `target_value` - (Required) The target value for the scaling policy.

### instance_requirements

* `architectures` - (Required) List of CPU architectures. Valid values are `["x86_64"]` and `["arm64"]`.
* `allowed_instance_types` - (Optional) List of allowed instance types (e.g., `["m5.xlarge"]`).
* `excluded_instance_types` - (Optional) List of excluded instance types. You can specify only one of `allowed_instance_types` or `excluded_instance_types`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Capacity Provider.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `update` - (Default `10m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_lambda_capacity_provider.example example
```
