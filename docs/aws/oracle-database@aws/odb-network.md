# Odb Network

Manage Odb Network resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_odb_network:
    example:
      display_name: odb-my-net
      availability_zone_id: use1-az6
      client_subnet_cidr: 10.2.0.0/24
      backup_subnet_cidr: 10.2.1.0/24
      s3_access: DISABLED
      zero_etl_access: DISABLED
      tags: 

resource:
  aws_odb_network:
    example:
      display_name: odb-my-net
      availability_zone_id: use1-az6
      client_subnet_cidr: 10.2.0.0/24
      backup_subnet_cidr: 10.2.1.0/24
      s3_access: ENABLED
      zero_etl_access: ENABLED
      tags: 
```
