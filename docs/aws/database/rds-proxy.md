# RDS Proxy

Create RDS Proxy for connection pooling using ytofu YAML.

## Basic Proxy

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
        - auth_scheme: SECRETS
          description: example
          iam_auth: DISABLED
          secret_arn: ${aws_secretsmanager_secret.example.arn}
      tags:
        Name: example
```

## Proxy Target Group

```yaml
resource:
  aws_db_proxy_default_target_group:
    example:
      db_proxy_name: ${aws_db_proxy.example.name}
      connection_pool_config:
        connection_borrow_timeout: 120
        max_connections_percent: 100
        max_idle_connections_percent: 50

  aws_db_proxy_target:
    example:
      db_proxy_name: ${aws_db_proxy.example.name}
      target_group_name: ${aws_db_proxy_default_target_group.example.name}
      db_instance_identifier: ${aws_db_instance.example.identifier}
```
