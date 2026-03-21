# RDS Custom DB Engine Version

Manage RDS Custom DB Engine Version resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:
      description: KMS symmetric key for RDS Custom for Oracle

resource:
  aws_rds_custom_db_engine_version:
    example:
      database_installation_files_s3_bucket_name: DOC-EXAMPLE-BUCKET
      database_installation_files_s3_prefix: 1915_GI/
      engine: custom-oracle-ee-cdb
      engine_version: 19.cdb_cev1
      kms_key_id: ${aws_kms_key.example.arn}
      manifest: |
        {
        "databaseInstallationFileNames":["V982063-01.zip"]
        }
      tags:
        Name: example
        Key: value
```

## RDS Custom for Oracle External Manifest Usage

```yaml
resource:
  aws_kms_key:
    example:
      description: KMS symmetric key for RDS Custom for Oracle

resource:
  aws_rds_custom_db_engine_version:
    example:
      database_installation_files_s3_bucket_name: DOC-EXAMPLE-BUCKET
      database_installation_files_s3_prefix: 1915_GI/
      engine: custom-oracle-ee-cdb
      engine_version: 19.cdb_cev1
      kms_key_id: ${aws_kms_key.example.arn}
      filename: manifest_1915_GI.json
      manifest_hash: ${filebase64sha256(manifest_1915_GI.json)}
      tags:
        Name: example
        Key: value
```

## RDS Custom for SQL Server Usage

```yaml
resource:
  aws_rds_custom_db_engine_version:
    test:
      engine: custom-sqlserver-se
      engine_version: 15.00.4249.2.cev-1
      source_image_id: ami-0aa12345678a12ab1
```

## RDS Custom for SQL Server Usage with AMI from another region

```yaml
resource:
  aws_ami_copy:
    example:
      name: sqlserver-se-2019-15.00.4249.2
      description: A copy of ami-xxxxxxxx
      source_ami_id: ami-xxxxxxxx
      source_ami_region: us-east-1

resource:
  aws_rds_custom_db_engine_version:
    test:
      engine: custom-sqlserver-se
      engine_version: 15.00.4249.2.cev-1
      source_image_id: ${aws_ami_copy.example.id}
```
