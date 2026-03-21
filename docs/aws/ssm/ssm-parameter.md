# SSM Parameter

Manage SSM Parameter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssm_parameter:
    foo:
      name: foo
      type: String
      value: bar
```

## Encrypted string using default SSM KMS key

```yaml
resource:
  aws_db_instance:
    default:
      allocated_storage: 10
      storage_type: gp2
      engine: mysql
      engine_version: 5.7.16
      instance_class: db.t2.micro
      db_name: mydb
      username: foo
      password: example-database_master_password
      db_subnet_group_name: my_database_subnet_group
      parameter_group_name: default.mysql5.7

resource:
  aws_ssm_parameter:
    secret:
      name: /production/database/password/master
      description: The parameter description
      type: SecureString
      value: example-database_master_password
      tags:
        environment: production
```
