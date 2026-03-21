# EC2 Traffic Mirror Target

Manage EC2 Traffic Mirror Target resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_traffic_mirror_target:
    nlb:
      description: NLB target
      network_load_balancer_arn: ${aws_lb.lb.arn}

resource:
  aws_ec2_traffic_mirror_target:
    eni:
      description: ENI target
      network_interface_id: ${aws_instance.test.primary_network_interface_id}

resource:
  aws_ec2_traffic_mirror_target:
    gwlb:
      description: GWLB target
      gateway_load_balancer_endpoint_id: ${aws_vpc_endpoint.example.id}
```
