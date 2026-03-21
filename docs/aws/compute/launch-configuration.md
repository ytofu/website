# Resource: aws_launch_configuration

Provides a resource to create a new launch configuration, used for autoscaling groups.

## Basic Example

```yaml
data:
  aws_ami:
    ubuntu:
      most_recent: true
      filter:
        name: name
        values: 
          - "ubuntu/images/hvm-ssd/ubuntu-trusty-14.04-amd64-server-*"
      filter:
        name: virtualization-type
        values: 
          - hvm
      owners: 
        - 099720109477

resource:
  aws_launch_configuration:
    as_conf:
      name: web_config
      image_id: ${data.aws_ami.ubuntu.id}
      instance_type: t2.micro
```

## Argument Reference

The following arguments are required:

* `image_id` - (Required) The EC2 image ID to launch.
* `instance_type` - (Required) The size of instance to launch.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `associate_public_ip_address` - (Optional) Associate a public ip address with an instance in a VPC.
* `ebs_block_device` - (Optional) Additional EBS block devices to attach to the instance. See [Block Devices](#block-devices) below for details.
* `ebs_optimized` - (Optional) If true, the launched EC2 instance will be EBS-optimized.
* `enable_monitoring` - (Optional) Enables/disables detailed monitoring. This is enabled by default.
* `ephemeral_block_device` - (Optional) Customize Ephemeral (also known as "Instance Store") volumes on the instance. See [Block Devices](#block-devices) below for details.
* `iam_instance_profile` - (Optional) The name attribute of the IAM instance profile to associate with launched instances.
* `key_name` - (Optional) The key name that should be used for the instance.
* `metadata_options` - The metadata options for the instance.
    * `http_endpoint` - The state of the metadata service: `enabled`, `disabled`.
    * `http_tokens` - If session tokens are required: `optional`, `required`.
    * `http_put_response_hop_limit` - The desired HTTP PUT response hop limit for instance metadata requests.
* `name` - (Optional) The name of the launch configuration. If you leave this blank, ytofu will auto-generate a unique name. Conflicts with `name_prefix`.
* `name_prefix` - (Optional) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `security_groups` - (Optional) A list of associated security group IDS.
* `placement_tenancy` - (Optional) The tenancy of the instance. Valid values are `default` or `dedicated`, see [AWS's Create Launch Configuration](http://docs.aws.amazon.com/AutoScaling/latest/APIReference/API_CreateLaunchConfiguration.html) for more details.
* `root_block_device` - (Optional) Customize details about the root block device of the instance. See [Block Devices](#block-devices) below for details.
* `spot_price` - (Optional; Default: On-demand price) The maximum price to use for reserving spot instances.
* `user_data` - (Optional) The user data to provide when launching the instance. Do not pass gzip-compressed data via this argument; see `user_data_base64` instead.
* `user_data_base64` - (Optional) Can be used instead of `user_data` to pass base64-encoded binary data directly. Use this instead of `user_data` whenever the value is not a valid UTF-8 string. For example, gzip-encoded user data must be base64-encoded and passed via this argument to avoid corruption.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the launch configuration.
* `arn` - The Amazon Resource Name of the launch configuration.
* `name` - The name of the launch configuration.

[1]: /docs/providers/aws/r/autoscaling_group.html
[2]: https://www.terraform.io/docs/configuration/meta-arguments/lifecycle.html
[3]: /docs/providers/aws/r/spot_instance_request.html

## Import

```bash
ytofu import aws_launch_configuration.as_conf terraform-lg-123456
```
