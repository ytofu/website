# Resource: aws_athena_prepared_statement

ytofu resource for managing an Athena Prepared Statement.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    test:
      bucket: tf-test
      force_destroy: true

  aws_athena_workgroup:
    test:
      name: tf-test

  aws_athena_database:
    test:
      name: example
      bucket: ${aws_s3_bucket.test.bucket}

  aws_athena_prepared_statement:
    test:
      name: tf_test
      query_statement: "SELECT * FROM ${aws_athena_database.test.name} WHERE x = ?"
      workgroup: ${aws_athena_workgroup.test.name}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the prepared statement. Maximum length of 256.
* `workgroup` - (Required) The name of the workgroup to which the prepared statement belongs.
* `query_statement` - (Required) The query string for the prepared statement.
* `description` - (Optional) Brief explanation of prepared statement. Maximum length of 1024.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the prepared statement

## Timeouts

Configuration options:

* `create` - (Default `60m`)
* `update` - (Default `180m`)
* `delete` - (Default `90m`)

## Import

```bash
ytofu import aws_athena_prepared_statement.example 12345abcde/example
```
