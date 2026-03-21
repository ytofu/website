# DB Parameter Group

Manage DB Parameter Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_db_parameter_group:
    default:
      name: rds-pg
      family: mysql5.6
      parameter:
        name: character_set_server
        value: utf8
      parameter:
        name: character_set_client
        value: utf8
```

## `create_before_destroy` Lifecycle Configuration

```yaml
resource:
  aws_db_parameter_group:
    example:
      name_prefix: my-pg
      family: postgres13
      parameter:
        name: log_connections
        value: 1
      lifecycle:
        create_before_destroy: true

resource:
  aws_db_instance:
    example:
      parameter_group_name: ${aws_db_parameter_group.example.name}
      apply_immediately: true
```

## Problematic Plan Changes

```yaml
resource:
  aws_db_parameter_group:
    test:
      name: random-test-parameter
      family: mysql5.7
      parameter:
        name: "default_password_lifetime" # same as AWS default
        value: "0"                         # same as AWS default
```
