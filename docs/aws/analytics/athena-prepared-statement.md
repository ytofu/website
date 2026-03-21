# Athena Prepared Statement

Manage Athena Prepared Statement resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    test:
      bucket: tf-test
      force_destroy: true

resource:
  aws_athena_workgroup:
    test:
      name: tf-test

resource:
  aws_athena_database:
    test:
      name: example
      bucket: ${aws_s3_bucket.test.bucket}

resource:
  aws_athena_prepared_statement:
    test:
      name: tf_test
      query_statement: "SELECT * FROM ${aws_athena_database.test.name} WHERE x = ?"
      workgroup: ${aws_athena_workgroup.test.name}
```
