# Elasticache Serverless Cache

Manage Elasticache Serverless Cache resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_elasticache_serverless_cache:
    example:
      engine: memcached
      name: example
      cache_usage_limits:
        data_storage:
          maximum: 10
          unit: GB
        ecpu_per_second:
          maximum: 5000
      description: Test Server
      kms_key_id: ${aws_kms_key.test.arn}
      major_engine_version: 1.6
      security_group_ids: 
        - ${aws_security_group.test.id}
      subnet_ids: ${aws_subnet.test[*].id}
```

## Redis OSS Serverless

```yaml
resource:
  aws_elasticache_serverless_cache:
    example:
      engine: redis
      name: example
      cache_usage_limits:
        data_storage:
          maximum: 10
          unit: GB
        ecpu_per_second:
          maximum: 5000
      daily_snapshot_time: "09:00"
      description: Test Server
      kms_key_id: ${aws_kms_key.test.arn}
      major_engine_version: 7
      snapshot_retention_limit: 1
      security_group_ids: 
        - ${aws_security_group.test.id}
      subnet_ids: ${aws_subnet.test[*].id}
```

## Valkey Serverless

```yaml
resource:
  aws_elasticache_serverless_cache:
    example:
      engine: valkey
      name: example
      cache_usage_limits:
        data_storage:
          maximum: 10
          unit: GB
        ecpu_per_second:
          maximum: 5000
      daily_snapshot_time: "09:00"
      description: Test Server
      kms_key_id: ${aws_kms_key.test.arn}
      major_engine_version: 7
      snapshot_retention_limit: 1
      security_group_ids: 
        - ${aws_security_group.test.id}
      subnet_ids: ${aws_subnet.test[*].id}
```
