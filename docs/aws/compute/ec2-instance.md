# EC2 Instance

Launch and manage Amazon EC2 virtual machines using ytofu YAML.

## Basic Example with AMI Lookup

```yaml
data:
  aws_ami:
    ubuntu:
      most_recent: true
      filter:
        - name: name
          values:
            - ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*
        - name: virtualization-type
          values:
            - hvm
      owners:
        - "099720109477"  # Canonical

resource:
  aws_instance:
    example:
      ami: ${data.aws_ami.ubuntu.id}
      instance_type: t3.micro
      tags:
        Name: HelloWorld
```

## Using Systems Manager Parameter Store

```yaml
resource:
  aws_instance:
    example:
      ami: resolve:ssm:/aws/service/ami-amazon-linux-latest/al2023-ami-kernel-default-x86_64
      instance_type: t3.micro
      tags:
        Name: HelloWorld
```

## Spot Instance

```yaml
data:
  aws_ami:
    example:
      most_recent: true
      owners:
        - amazon
      filter:
        - name: architecture
          values:
            - arm64
        - name: name
          values:
            - al2023-ami-2023*

resource:
  aws_instance:
    example:
      ami: ${data.aws_ami.example.id}
      instance_type: t4g.nano
      instance_market_options:
        market_type: spot
        spot_options:
          max_price: "0.0031"
      tags:
        Name: test-spot
```

## With Network Interface and Credit Specification

```yaml
resource:
  aws_vpc:
    my_vpc:
      cidr_block: 172.16.0.0/16
      tags:
        Name: tf-example

  aws_subnet:
    my_subnet:
      vpc_id: ${aws_vpc.my_vpc.id}
      cidr_block: 172.16.10.0/24
      availability_zone: us-west-2a
      tags:
        Name: tf-example

  aws_network_interface:
    example:
      subnet_id: ${aws_subnet.my_subnet.id}
      private_ips:
        - 172.16.10.100
      tags:
        Name: primary_network_interface

  aws_instance:
    example:
      ami: ami-005e54dee72cc1d00
      instance_type: t2.micro
      primary_network_interface:
        network_interface_id: ${aws_network_interface.example.id}
      credit_specification:
        cpu_credits: unlimited
```

## With CPU Options

```yaml
data:
  aws_ami:
    amzn_linux_2023:
      most_recent: true
      owners:
        - amazon
      filter:
        - name: name
          values:
            - al2023-ami-2023.*-x86_64

resource:
  aws_vpc:
    example:
      cidr_block: 172.16.0.0/16
      tags:
        Name: tf-example

  aws_subnet:
    example:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 172.16.10.0/24
      availability_zone: us-east-2a
      tags:
        Name: tf-example

  aws_instance:
    example:
      ami: ${data.aws_ami.amzn_linux_2023.id}
      instance_type: c6a.2xlarge
      subnet_id: ${aws_subnet.example.id}
      cpu_options:
        core_count: 2
        threads_per_core: 2
      tags:
        Name: tf-example
```

## Host Resource Group

```yaml
resource:
  aws_instance:
    this:
      ami: ami-0dcc1e21636832c5d
      instance_type: m5.large
      host_resource_group_arn: arn:aws:resource-groups:us-west-2:123456789012:group/win-testhost
      tenancy: host
```

## Arguments Reference

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| ami | string | Yes | Amazon Machine Image ID |
| instance_type | string | Yes | Instance type (e.g., t3.micro) |
| subnet_id | string | No | VPC subnet to launch in |
| vpc_security_group_ids | list | No | Security group IDs |
| key_name | string | No | SSH key pair name |
| iam_instance_profile | string | No | IAM instance profile |
| user_data | string | No | Startup script (base64 encoded) |
| root_block_device | object | No | Root volume configuration |
| ebs_block_device | list | No | Additional EBS volumes |
| instance_market_options | object | No | Spot instance options |
| cpu_options | object | No | CPU core and thread settings |
| credit_specification | object | No | CPU credits for burstable instances |
| metadata_options | object | No | Instance metadata service config |
| tags | map | No | Resource tags |

## Common Patterns

### Web Server with User Data

```yaml
resource:
  aws_instance:
    web:
      ami: ${data.aws_ami.ubuntu.id}
      instance_type: t3.small
      subnet_id: ${aws_subnet.public.id}
      vpc_security_group_ids:
        - ${aws_security_group.web.id}
      user_data: |
        #!/bin/bash
        apt-get update -y
        apt-get install -y nginx
        systemctl start nginx
        systemctl enable nginx
        echo "Hello from ytofu!" > /var/www/html/index.html
      tags:
        Name: web-server
```

### Instance with Multiple EBS Volumes

```yaml
resource:
  aws_instance:
    database:
      ami: ${data.aws_ami.ubuntu.id}
      instance_type: r5.large
      root_block_device:
        volume_size: 50
        volume_type: gp3
        encrypted: true
      ebs_block_device:
        - device_name: /dev/sdf
          volume_size: 100
          volume_type: gp3
          encrypted: true
          delete_on_termination: false
        - device_name: /dev/sdg
          volume_size: 500
          volume_type: st1
          encrypted: true
      tags:
        Name: database-server
```

### Instance with IAM Role

```yaml
resource:
  aws_iam_role:
    ec2_role:
      name: ec2-s3-access
      assume_role_policy: |
        {
          "Version": "2012-10-17",
          "Statement": [{
            "Action": "sts:AssumeRole",
            "Principal": {"Service": "ec2.amazonaws.com"},
            "Effect": "Allow"
          }]
        }

  aws_iam_instance_profile:
    ec2_profile:
      name: ec2-s3-access
      role: ${aws_iam_role.ec2_role.name}

  aws_instance:
    app:
      ami: ${data.aws_ami.ubuntu.id}
      instance_type: t3.micro
      iam_instance_profile: ${aws_iam_instance_profile.ec2_profile.name}
      tags:
        Name: app-server
```

## Attributes Reference

| Attribute | Description |
|-----------|-------------|
| id | Instance ID |
| arn | Instance ARN |
| public_ip | Public IP address |
| private_ip | Private IP address |
| public_dns | Public DNS name |
| private_dns | Private DNS name |

## Best Practices

- **Use AMI data source** to get latest AMI IDs dynamically
- **Use SSM Parameter Store** for Amazon Linux AMIs
- **Enable IMDSv2** for enhanced metadata security
- **Use gp3 volumes** instead of gp2 for better price/performance
- **Encrypt all EBS volumes** for data security
- **Use Spot Instances** for fault-tolerant workloads to reduce costs
- **Tag all instances** for cost allocation and management

## Related Resources

- [Launch Template](launch-template.md)
- [Auto Scaling](autoscaling.md)
- [Security Groups](../networking/security-groups.md)
- [VPC](../networking/vpc.md)
