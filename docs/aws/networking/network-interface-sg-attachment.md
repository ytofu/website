# Resource: aws_network_interface_sg_attachment

This resource attaches a security group to an Elastic Network Interface (ENI).
It can be used to attach a security group to any existing ENI, be it a
secondary ENI or one attached as the primary interface on an instance.

## Basic Example

```yaml
data:
  aws_ami:
    ami:
      most_recent: true
      filter:
        name: name
        values: 
          - "amzn-ami-hvm-*"
      owners: 
        - amazon

resource:
  aws_instance:
    instance:
      instance_type: t2.micro
      ami: ${data.aws_ami.ami.id}
      tags:
        type: terraform-test-instance

  aws_security_group:
    sg:
      tags:
        type: terraform-test-security-group

  aws_network_interface_sg_attachment:
    sg_attachment:
      security_group_id: ${aws_security_group.sg.id}
      network_interface_id: ${aws_instance.instance.primary_network_interface_id}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `security_group_id` - (Required) The ID of the security group.
* `network_interface_id` - (Required) The ID of the network interface to attach to.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

- `create` - (Default `3m`)
- `read` - (Default `3m`)
- `delete` - (Default `3m`)

## Import

```bash
ytofu import aws_network_interface_sg_attachment.sg_attachment eni-1234567890abcdef0_sg-1234567890abcdef0
```
