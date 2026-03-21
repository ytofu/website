# Opensearchserverless VPC Endpoint

Manage Opensearchserverless VPC Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_opensearchserverless_vpc_endpoint:
    example:
      name: myendpoint
      subnet_ids: 
        - ${aws_subnet.example.id}
      vpc_id: ${aws_vpc.example.id}
```
