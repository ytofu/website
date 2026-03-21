# EC2 Instance State

Manage EC2 Instance State resources using ytofu YAML.

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

resource:
  aws_ec2_instance_state:
    test:
      instance_id: ${aws_instance.test.id}
      state: stopped
```
