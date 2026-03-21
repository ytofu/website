# RDS DB Instance

Create and manage RDS database instances using ytofu YAML.

## Basic MySQL Instance

```yaml
resource:
  aws_db_instance:
    default:
      allocated_storage: 10
      db_name: mydb
      engine: mysql
      engine_version: "8.0"
      instance_class: db.t3.micro
      username: foo
      password: foobarbaz
      parameter_group_name: default.mysql8.0
      skip_final_snapshot: true
```

## PostgreSQL Instance

```yaml
resource:
  aws_db_instance:
    postgres:
      allocated_storage: 20
      db_name: mydb
      engine: postgres
      engine_version: "16"
      instance_class: db.t3.micro
      username: postgres
      password: example-db_password
      parameter_group_name: default.postgres16
      skip_final_snapshot: true
      tags:
        Name: PostgreSQL Database
```

## With Multi-AZ

```yaml
resource:
  aws_db_instance:
    production:
      allocated_storage: 100
      storage_type: gp3
      engine: mysql
      engine_version: "8.0"
      instance_class: db.r6g.large
      db_name: production
      username: admin
      password: example-db_password
      multi_az: true
      backup_retention_period: 7
      backup_window: 03:00-04:00
      maintenance_window: Mon:04:00-Mon:05:00
      storage_encrypted: true
      deletion_protection: true
      skip_final_snapshot: false
      final_snapshot_identifier: production-final
      tags:
        Environment: production
```

## With Subnet Group and Security Group

```yaml
resource:
  aws_db_subnet_group:
    default:
      name: main
      subnet_ids:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
      tags:
        Name: My DB subnet group

  aws_db_instance:
    default:
      allocated_storage: 20
      engine: mysql
      engine_version: "8.0"
      instance_class: db.t3.micro
      db_name: mydb
      username: admin
      password: example-db_password
      db_subnet_group_name: ${aws_db_subnet_group.default.name}
      vpc_security_group_ids:
        - ${aws_security_group.db.id}
      skip_final_snapshot: true
```

## Read Replica

```yaml
resource:
  aws_db_instance:
    replica:
      replicate_source_db: ${aws_db_instance.default.identifier}
      instance_class: db.t3.micro
      skip_final_snapshot: true
```
