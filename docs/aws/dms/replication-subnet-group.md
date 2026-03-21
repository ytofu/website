# DMS Replication Subnet Group

Create subnet groups for DMS replication instances using ytofu YAML.

## Basic Subnet Group

```yaml
resource:
  aws_dms_replication_subnet_group:
    example:
      replication_subnet_group_description: Example DMS subnet group
      replication_subnet_group_id: example
      subnet_ids:
        - ${aws_subnet.private_a.id}
        - ${aws_subnet.private_b.id}
```
