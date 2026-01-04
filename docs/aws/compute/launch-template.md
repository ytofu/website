# Launch Template

Create reusable EC2 instance configurations with Launch Templates using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_launch_template:
    web:
      name: web-template
      image_id: ami-0c55b159cbfafe1f0
      instance_type: t3.micro
```

## Complete Launch Template

```yaml
resource:
  aws_launch_template:
    web:
      name: web-template
      image_id: ami-0c55b159cbfafe1f0
      instance_type: t3.micro
      key_name: my-key

      vpc_security_group_ids:
        - ${aws_security_group.web.id}

      iam_instance_profile:
        arn: ${aws_iam_instance_profile.web.arn}

      block_device_mappings:
        - device_name: /dev/xvda
          ebs:
            volume_size: 20
            volume_type: gp3
            encrypted: true
            delete_on_termination: true

      monitoring:
        enabled: true

      metadata_options:
        http_endpoint: enabled
        http_tokens: required
        http_put_response_hop_limit: 1

      user_data: ${base64encode(file("userdata.sh"))}

      tag_specifications:
        - resource_type: instance
          tags:
            Name: web-server
            Environment: production

        - resource_type: volume
          tags:
            Name: web-volume

      tags:
        Name: web-template
```

## Arguments Reference

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| name | string | No | Template name |
| name_prefix | string | No | Name prefix |
| image_id | string | No | AMI ID |
| instance_type | string | No | Instance type |
| key_name | string | No | SSH key name |
| vpc_security_group_ids | list | No | Security group IDs |
| iam_instance_profile | object | No | IAM profile |
| block_device_mappings | list | No | EBS volumes |
| network_interfaces | list | No | Network configuration |
| monitoring | object | No | Detailed monitoring |
| metadata_options | object | No | Instance metadata config |
| user_data | string | No | Base64-encoded user data |
| tag_specifications | list | No | Resource tags |
| tags | map | No | Template tags |

## Common Patterns

### Web Server Template

```yaml
resource:
  aws_launch_template:
    web:
      name: web-server
      image_id: ami-0c55b159cbfafe1f0
      instance_type: t3.small

      vpc_security_group_ids:
        - ${aws_security_group.web.id}

      iam_instance_profile:
        arn: ${aws_iam_instance_profile.web.arn}

      block_device_mappings:
        - device_name: /dev/xvda
          ebs:
            volume_size: 30
            volume_type: gp3
            throughput: 125
            iops: 3000
            encrypted: true

      user_data: |
        ${base64encode(<<-EOF
          #!/bin/bash
          yum update -y
          yum install -y httpd
          systemctl start httpd
          systemctl enable httpd
          echo "Hello from $(hostname)" > /var/www/html/index.html
        EOF
        )}

      tag_specifications:
        - resource_type: instance
          tags:
            Name: web-server
        - resource_type: volume
          tags:
            Name: web-volume
```

### Mixed Instances (Spot + On-Demand)

```yaml
resource:
  aws_launch_template:
    mixed:
      name: mixed-instances
      image_id: ami-0c55b159cbfafe1f0

      # Don't specify instance_type here - use in ASG

      vpc_security_group_ids:
        - ${aws_security_group.app.id}

  aws_autoscaling_group:
    mixed:
      name: mixed-asg
      vpc_zone_identifier:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
      desired_capacity: 4
      min_size: 2
      max_size: 10

      mixed_instances_policy:
        instances_distribution:
          on_demand_base_capacity: 2
          on_demand_percentage_above_base_capacity: 25
          spot_allocation_strategy: capacity-optimized

        launch_template:
          launch_template_specification:
            launch_template_id: ${aws_launch_template.mixed.id}
            version: $Latest

          override:
            - instance_type: t3.medium
            - instance_type: t3.large
            - instance_type: t3a.medium
            - instance_type: t3a.large
```

### Template with Network Interface

```yaml
resource:
  aws_launch_template:
    with_eni:
      name: with-eni
      image_id: ami-0c55b159cbfafe1f0
      instance_type: t3.micro

      network_interfaces:
        - device_index: 0
          associate_public_ip_address: true
          security_groups:
            - ${aws_security_group.web.id}
          delete_on_termination: true
```

### ECS-Optimized Template

```yaml
resource:
  aws_launch_template:
    ecs:
      name: ecs-node
      image_id: ${data.aws_ami.ecs_optimized.id}
      instance_type: t3.medium

      iam_instance_profile:
        arn: ${aws_iam_instance_profile.ecs.arn}

      vpc_security_group_ids:
        - ${aws_security_group.ecs.id}

      user_data: |
        ${base64encode(<<-EOF
          #!/bin/bash
          echo ECS_CLUSTER=${aws_ecs_cluster.main.name} >> /etc/ecs/ecs.config
        EOF
        )}

      tag_specifications:
        - resource_type: instance
          tags:
            Name: ecs-node

data:
  aws_ami:
    ecs_optimized:
      most_recent: true
      owners:
        - amazon

      filter:
        - name: name
          values:
            - amzn2-ami-ecs-hvm-*-x86_64-ebs
```

### IMDSv2 Enforced

```yaml
resource:
  aws_launch_template:
    secure:
      name: secure-template
      image_id: ami-0c55b159cbfafe1f0
      instance_type: t3.micro

      metadata_options:
        http_endpoint: enabled
        http_tokens: required  # Enforces IMDSv2
        http_put_response_hop_limit: 1
        instance_metadata_tags: enabled
```

## Using with Auto Scaling

```yaml
resource:
  aws_launch_template:
    app:
      name: app-template
      image_id: ami-0c55b159cbfafe1f0
      instance_type: t3.micro

  aws_autoscaling_group:
    app:
      name: app-asg
      vpc_zone_identifier:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
      desired_capacity: 2
      min_size: 1
      max_size: 5

      launch_template:
        id: ${aws_launch_template.app.id}
        version: $Latest  # or $Default or specific version
```

## Versioning

```yaml
resource:
  aws_launch_template:
    app:
      name: app-template
      image_id: ami-0c55b159cbfafe1f0
      instance_type: t3.micro

      # Create new version on change
      update_default_version: true

output:
  latest_version:
    value: ${aws_launch_template.app.latest_version}

  default_version:
    value: ${aws_launch_template.app.default_version}
```

## Attributes Reference

| Attribute | Description |
|-----------|-------------|
| id | Launch template ID |
| arn | Launch template ARN |
| latest_version | Latest version number |
| default_version | Default version number |

## Best Practices

- **Use launch templates** instead of launch configurations
- **Enable IMDSv2** for security
- **Use versioning** for safe updates
- **Encrypt EBS volumes** by default
- **Set appropriate metadata hop limit**
- **Tag all resources** via tag_specifications
- **Use $Latest or $Default** version references
- **Enable detailed monitoring** for production

## Launch Template vs Launch Configuration

| Feature | Launch Template | Launch Configuration |
|---------|-----------------|----------------------|
| Versioning | Yes | No |
| Multiple instance types | Yes | No |
| Spot options | Full support | Limited |
| T2/T3 Unlimited | Yes | No |
| Placement groups | Yes | Limited |
| Recommended | Yes | Deprecated |

## Related Resources

- [Auto Scaling](autoscaling.md)
- [EC2 Instance](ec2-instance.md)
- [Security Groups](../networking/security-groups.md)
