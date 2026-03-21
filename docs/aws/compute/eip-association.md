# Resource: aws_eip_association

Provides an AWS EIP Association as a top level resource, to associate and disassociate Elastic IPs from AWS Instances and Network Interfaces.

## Basic Example

```yaml
resource:
  aws_eip_association:
    eip_assoc:
      instance_id: ${aws_instance.web.id}
      allocation_id: ${aws_eip.example.id}

resource:
  aws_instance:
    web:
      ami: ami-21f78e11
      availability_zone: us-west-2a
      instance_type: t2.micro
      tags:
        Name: HelloWorld

resource:
  aws_eip:
    example:
      domain: vpc
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `allocation_id` - (Optional, Forces new resource) ID of the associated Elastic IP.
  This argument is required despite being optional at the resource level due to legacy support for EC2-Classic networking.
* `allow_reassociation` - (Optional, Forces new resource) Whether to allow an Elastic IP address to be re-associated.
  Defaults to `true`.
* `instance_id` - (Optional, Forces new resource) ID of the instance.
  The instance must have exactly one attached network interface.
  You can specify either the instance ID or the network interface ID, but not both.
* `network_interface_id` - (Optional, Forces new resource) ID of the network interface.
  If the instance has more than one network interface, you must specify a network interface ID.
  You can specify either the instance ID or the network interface ID, but not both.
* `private_ip_address` - (Optional, Forces new resource) Primary or secondary private IP address to associate with the Elastic IP address.
  If no private IP address is specified, the Elastic IP address is associated with the primary private IP address.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID that represents the association of the Elastic IP address with an instance.

## Import

```bash
ytofu import aws_eip_association.test eipassoc-ab12c345
```
