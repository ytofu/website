# EIP Association

Manage EIP Association resources using ytofu YAML.

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
