# DB Proxy Target

Manage DB Proxy Target resources using ytofu YAML.

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

resource:
  aws_db_proxy_default_target_group:
    example:
      db_proxy_name: ${aws_db_proxy.example.name}
      connection_pool_config:
        connection_borrow_timeout: 120
        init_query: SET x=1, y=2
        max_connections_percent: 100
        max_idle_connections_percent: 50
        session_pinning_filters: 
          - EXCLUDE_VARIABLE_SETS
      lifecycle:
        replace_triggered_by: 
          - ${aws_db_proxy.example.id}

resource:
  aws_db_proxy_target:
    example:
      db_instance_identifier: ${aws_db_instance.example.identifier}
      db_proxy_name: ${aws_db_proxy.example.name}
      target_group_name: ${aws_db_proxy_default_target_group.example.name}
      lifecycle:
        replace_triggered_by: 
          - ${aws_db_proxy.example.id}
```
