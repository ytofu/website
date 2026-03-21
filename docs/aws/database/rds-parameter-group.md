# RDS Parameter Group

Configure database parameter groups using ytofu YAML.

## MySQL Parameter Group

```yaml
resource:
  aws_db_parameter_group:
    default:
      name: rds-pg
      family: mysql8.0
      parameter:
        - name: character_set_server
          value: utf8
        - name: character_set_client
          value: utf8
```

## PostgreSQL Parameter Group

```yaml
resource:
  aws_db_parameter_group:
    postgres:
      name: postgres-pg
      family: postgres16
      parameter:
        - name: log_connections
          value: "1"
        - name: log_disconnections
          value: "1"
```
