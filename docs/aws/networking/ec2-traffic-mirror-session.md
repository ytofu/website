# EC2 Traffic Mirror Session

Manage EC2 Traffic Mirror Session resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_traffic_mirror_filter:
    filter:
      description: traffic mirror filter - terraform example
      network_services: 
        - amazon-dns

resource:
  aws_ec2_traffic_mirror_target:
    target:
      network_load_balancer_arn: ${aws_lb.lb.arn}

resource:
  aws_ec2_traffic_mirror_session:
    session:
      description: traffic mirror session - terraform example
      network_interface_id: ${aws_instance.test.primary_network_interface_id}
      session_number: 1
      traffic_mirror_filter_id: ${aws_ec2_traffic_mirror_filter.filter.id}
      traffic_mirror_target_id: ${aws_ec2_traffic_mirror_target.target.id}
```
