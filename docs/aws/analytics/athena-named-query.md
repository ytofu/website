# Resource: aws_athena_named_query

Provides an Athena Named Query resource.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    hoge:
      bucket: tf-test

  aws_kms_key:
    test:
      deletion_window_in_days: 7
      description: Athena KMS Key

  aws_athena_workgroup:
    test:
      name: example
      configuration:
        result_configuration:
          encryption_configuration:
            encryption_option: SSE_KMS
            kms_key_arn: ${aws_kms_key.test.arn}

  aws_athena_database:
    hoge:
      name: users
      bucket: ${aws_s3_bucket.hoge.id}

  aws_athena_named_query:
    foo:
      name: bar
      workgroup: ${aws_athena_workgroup.test.id}
      database: ${aws_athena_database.hoge.name}
      query: "SELECT * FROM ${aws_athena_database.hoge.name} limit 10;"```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Plain language name for the query. Maximum length of 128.
* `workgroup` - (Optional) Workgroup to which the query belongs. Defaults to `primary`
* `database` - (Required) Database to which the query belongs.
* `query` - (Required) Text of the query itself. In other words, all query statements. Maximum length of 262144.
* `description` - (Optional) Brief explanation of the query. Maximum length of 1024.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Unique ID of the query.

## Import

```bash
ytofu import aws_athena_named_query.example 0123456789
```
