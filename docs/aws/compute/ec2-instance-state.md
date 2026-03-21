# Resource: aws_ec2_instance_state

Provides an EC2 instance state resource. This allows managing an instance power state.

## Basic Example

```yaml
data:
  aws_ami:
    ubuntu:
      most_recent: true
      filter:
        name: name
        values: 
          - "ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"
      filter:
        name: virtualization-type
        values: 
          - hvm
      owners: 
        - 099720109477

resource:
  aws_instance:
    test:
      ami: ${data.aws_ami.ubuntu.id}
      instance_type: t3.micro
      tags:
        Name: HelloWorld

  aws_ec2_instance_state:
    test:
      instance_id: ${aws_instance.test.id}
      state: stopped```

## Argument Reference

The following arguments are required:

* `instance_id` - (Required) ID of the instance.
* `state` - (Required) - State of the instance. Valid values are `stopped`, `running`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `force` - (Optional) Whether to request a forced stop when `state` is `stopped`. Otherwise (_i.e._, `state` is `running`), ignored. When an instance is forced to stop, it does not flush file system caches or file system metadata, and you must subsequently perform file system check and repair. Not recommended for Windows instances. Defaults to `false`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the instance (matches `instance_id`).

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `update` - (Default `10m`)
* `delete` - (Default `1m`)

## Import

```bash
ytofu import aws_ec2_instance_state.test i-02cae6557dfcf2f96
```
