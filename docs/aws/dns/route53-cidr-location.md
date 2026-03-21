# Route53 CIDR Location

Manage Route53 CIDR Location resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_cidr_collection:
    example:
      name: collection-1

resource:
  aws_route53_cidr_location:
    example:
      cidr_collection_id: ${aws_route53_cidr_collection.example.id}
      name: office
      cidr_blocks: 
        - 200.5.3.0/24
        - 200.6.3.0/24
```
