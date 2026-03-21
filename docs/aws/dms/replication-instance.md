# DMS Replication Instance

Create replication instances for database migration using ytofu YAML.

## Basic Instance

```yaml
resource:
  aws_dms_replication_instance:
    example:
      allocated_storage: 20
      apply_immediately: true
      auto_minor_version_upgrade: true
      multi_az: false
      publicly_accessible: false
      replication_instance_class: dms.t3.micro
      replication_instance_id: example
      replication_subnet_group_id: ${aws_dms_replication_subnet_group.example.id}
      vpc_security_group_ids:
        - ${aws_security_group.dms.id}
      tags:
        Name: example
```
