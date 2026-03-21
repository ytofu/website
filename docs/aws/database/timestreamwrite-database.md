# Resource: aws_timestreamwrite_database

Provides a Timestream database resource.

## Basic Example

```yaml
resource:
  aws_timestreamwrite_database:
    example:
      database_name: database-example
```

## Full usage

```yaml
resource:
  aws_timestreamwrite_database:
    example:
      database_name: database-example
      kms_key_id: ${aws_kms_key.example.arn}
      tags:
        Name: value
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `database_name` - (Required) The name of the Timestream database. Minimum length of 3. Maximum length of 64.
* `kms_key_id` - (Optional) The ARN (not Alias ARN) of the KMS key to be used to encrypt the data stored in the database. If the KMS key is not specified, the database will be encrypted with a Timestream managed KMS key located in your account. Refer to [AWS managed KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#aws-managed-cmk) for more info.
* `tags` - (Optional) Map of tags to assign to this resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the Timestream database.
* `arn` - The ARN that uniquely identifies this database.
* `kms_key_id` - The ARN of the KMS key used to encrypt the data stored in the database.
* `table_count` - The total number of tables found within the Timestream database.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_timestreamwrite_database.example example
```
