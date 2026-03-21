# DMS Endpoint

Create source and target endpoints for DMS using ytofu YAML.

## MySQL Source Endpoint

```yaml
resource:
  aws_dms_endpoint:
    source:
      endpoint_id: source-mysql
      endpoint_type: source
      engine_name: mysql
      server_name: source-db.example.com
      port: 3306
      username: admin
      password: example-db_password
      database_name: mydb
```

## S3 Target Endpoint

```yaml
resource:
  aws_dms_endpoint:
    target:
      endpoint_id: target-s3
      endpoint_type: target
      engine_name: s3
      s3_settings:
        bucket_name: ${aws_s3_bucket.example.bucket}
        service_access_role_arn: ${aws_iam_role.dms.arn}
        data_format: parquet
```

## PostgreSQL Endpoint

```yaml
resource:
  aws_dms_endpoint:
    postgres:
      endpoint_id: postgres-target
      endpoint_type: target
      engine_name: postgres
      server_name: ${aws_db_instance.postgres.address}
      port: 5432
      username: admin
      password: example-db_password
      database_name: mydb
      ssl_mode: require
```
