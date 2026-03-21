# EC2 Traffic Mirror Filter

Manage EC2 Traffic Mirror Filter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ec2_traffic_mirror_filter:
    foo:
      description: traffic mirror filter - terraform example
      network_services: 
        - amazon-dns
```
