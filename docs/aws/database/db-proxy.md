# DB Proxy

Manage DB Proxy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_db_proxy:
    example:
      name: example
      debug_logging: false
      engine_family: MYSQL
      idle_client_timeout: 1800
      require_tls: true
      role_arn: ${aws_iam_role.example.arn}
      vpc_security_group_ids: 
        - ${aws_security_group.example.id}
      vpc_subnet_ids: 
        - ${aws_subnet.example.id}
      auth:
        auth_scheme: SECRETS
        description: example
        iam_auth: DISABLED
        secret_arn: ${aws_secretsmanager_secret.example.arn}
      tags:
        Name: example
        Key: value
```

## Unsupported Availability Zones

```yaml
data:
  aws_availability_zones:
    available:
      exclude_zone_ids: 
        - use1-az3
      state: available
      filter:
        name: opt-in-status
        values: 
          - opt-in-not-required

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_subnet:
    example:
      cidr_block: 10.0.1.0/24
      availability_zone: ${data.aws_availability_zones.available.names[count.index]}
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_db_proxy:
    example:
      name: example
      vpc_subnet_ids: 
        - ${aws_subnet.example.id}
```
