# Instance

Manage Instance resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_ami:
    ubuntu:
      most_recent: true
      filter:
        name: name
        values: 
          - "ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*"
      filter:
        name: virtualization-type
        values: 
          - hvm
      owners: 
        - 099720109477

resource:
  aws_instance:
    example:
      ami: ${data.aws_ami.ubuntu.id}
      instance_type: t3.micro
      tags:
        Name: HelloWorld
```

## Spot instance example

```yaml
data:
  aws_ami:
    example:
      most_recent: true
      owners: 
        - amazon
      filter:
        name: architecture
        values: 
          - arm64
      filter:
        name: name
        values: 
          - "al2023-ami-2023*"

resource:
  aws_instance:
    example:
      ami: ${data.aws_ami.example.id}
      instance_market_options:
        market_type: spot
        spot_options:
          max_price: 0.0031
      instance_type: t4g.nano
      tags:
        Name: test-spot
```

## Network and credit specification example

```yaml
resource:
  aws_vpc:
    my_vpc:
      cidr_block: 172.16.0.0/16
      tags:
        Name: tf-example

resource:
  aws_subnet:
    my_subnet:
      vpc_id: ${aws_vpc.my_vpc.id}
      cidr_block: 172.16.10.0/24
      availability_zone: us-west-2a
      tags:
        Name: tf-example

resource:
  aws_network_interface:
    example:
      subnet_id: ${aws_subnet.my_subnet.id}
      private_ips: 
        - 172.16.10.100
      tags:
        Name: primary_network_interface

resource:
  aws_instance:
    example:
      ami: "ami-005e54dee72cc1d00" # us-west-2
      instance_type: t2.micro
      primary_network_interface:
        network_interface_id: ${aws_network_interface.example.id}
      credit_specification:
        cpu_credits: unlimited
```

## CPU options example

```yaml
resource:
  aws_vpc:
    example:
      cidr_block: 172.16.0.0/16
      tags:
        Name: tf-example

resource:
  aws_subnet:
    example:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 172.16.10.0/24
      availability_zone: us-east-2a
      tags:
        Name: tf-example

data:
  aws_ami:
    amzn-linux-2023-ami:
      most_recent: true
      owners: 
        - amazon
      filter:
        name: name
        values: 
          - "al2023-ami-2023.*-x86_64"

resource:
  aws_instance:
    example:
      ami: ${data.aws_ami.amzn-linux-2023-ami.id}
      instance_type: c6a.2xlarge
      subnet_id: ${aws_subnet.example.id}
      cpu_options:
        core_count: 2
        threads_per_core: 2
      tags:
        Name: tf-example
```

## Host resource group or License Manager registered AMI example

```yaml
resource:
  aws_instance:
    this:
      ami: ami-0dcc1e21636832c5d
      instance_type: m5.large
      host_resource_group_arn: "arn:aws:resource-groups:us-west-2:123456789012:group/win-testhost"
      tenancy: host
```
