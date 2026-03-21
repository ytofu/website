# Resource: aws_m2_environment

ytofu resource for managing an [AWS Mainframe Modernization Environment](https://docs.aws.amazon.com/m2/latest/userguide/environments-m2.html).

## Basic Example

```yaml
resource:
  aws_m2_environment:
    test:
      name: test-env
      engine_type: bluage
      instance_type: M2.m5.large
      security_groups: 
        - sg-01234567890abcdef
      subnet_ids: 
        - subnet-01234567890abcdef
        - subnet-01234567890abcdea
```

## High Availability

```yaml
resource:
  aws_m2_environment:
    test:
      name: test-env
      engine_type: bluage
      instance_type: M2.m5.large
      security_groups: 
        - sg-01234567890abcdef
      subnet_ids: 
        - subnet-01234567890abcdef
        - subnet-01234567890abcdea
      high_availability_config:
        desired_capacity: 2
```

## EFS Filesystem

```yaml
resource:
  aws_m2_environment:
    test:
      name: test-env
      engine_type: bluage
      instance_type: M2.m5.large
      security_groups: 
        - sg-01234567890abcdef
      subnet_ids: 
        - subnet-01234567890abcdef
        - subnet-01234567890abcdea
      storage_configuration:
        efs:
          file_system_id: fs-01234567890abcdef
          mount_point: /m2/mount/example
```

## FSX Filesystem

```yaml
resource:
  aws_m2_environment:
    test:
      name: test-env
      engine_type: bluage
      instance_type: M2.m5.large
      security_groups: 
        - sg-01234567890abcdef
      subnet_ids: 
        - subnet-01234567890abcdef
        - subnet-01234567890abcdea
      storage_configuration:
        fsx:
          file_system_id: fs-01234567890abcdef
          mount_point: /m2/mount/example
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the runtime environment. Must be unique within the account.
* `engine_type` - (Required) Engine type must be `microfocus` or `bluage`.
* `instance_type` - (Required) M2 Instance Type.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `engine_version` - (Optional) The specific version of the engine for the Environment.
* `force_update` - (Optional) Force update the environment even if applications are running.
* `kms_key_id` - (Optional) ARN of the KMS key to use for the Environment.
* `preferred_maintenance_window` - (Optional) Configures the maintenance window that you want for the runtime environment. The maintenance window must have the format `ddd:hh24:mi-ddd:hh24:mi` and must be less than 24 hours. If not provided a random value will be used.
* `publicly_accessible` - (Optional) Allow applications deployed to this environment to be publicly accessible.
* `security_group_ids` - (Optional) List of security group ids.
* `subnet_ids` - (Optional) List of subnet ids to deploy environment to.
* `tags` - (Optional) Key-value tags for the place index. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### storage_configuration

#### efs

This argument is processed in attribute-as-blocks mode.

The following arguments are required:

* `mount_point` - (Required) Path to mount the filesystem on, must start with `/m2/mount/`.
* `file_system_id` - (Required) Id of the EFS filesystem to mount.

#### fsx

This argument is processed in attribute-as-blocks mode.

The following arguments are required:

* `mount_point` - (Required) Path to mount the filesystem on, must start with `/m2/mount/`.
* `file_system_id` - (Required) Id of the FSX filesystem to mount.

### high_availability_config

This argument is processed in attribute-as-blocks mode.

The following arguments are required:

* `desired_capacity` - (Required) Desired number of instances for the Environment.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Environment.
* `id` - The id of the Environment.
* `environment_id` - The id of the Environment.
* `load_balancer_arn` - ARN of the load balancer created by the Environment.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_m2_environment.example 01234567890abcdef012345678
```
