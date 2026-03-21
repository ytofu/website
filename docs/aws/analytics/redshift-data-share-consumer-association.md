# Resource: aws_redshift_data_share_consumer_association

ytofu resource for managing an AWS Redshift Data Share Consumer Association.

## Basic Example

```yaml
resource:
  aws_redshift_data_share_consumer_association:
    example:
      data_share_arn: "arn:aws:redshift:us-west-2:123456789012:datashare:b3bfde75-73fd-408b-9086-d6fccfd6d588/example"
      associate_entire_account: true
```

## Consumer Region

```yaml
resource:
  aws_redshift_data_share_consumer_association:
    example:
      data_share_arn: "arn:aws:redshift:us-west-2:123456789012:datashare:b3bfde75-73fd-408b-9086-d6fccfd6d588/example"
      consumer_region: us-west-2
```

## Argument Reference

The following arguments are required:

* `data_share_arn` - (Required) Amazon Resource Name (ARN) of the datashare that the consumer is to use with the account or the namespace.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `allow_writes` - (Optional) Whether to allow write operations for a datashare.
* `associate_entire_account` - (Optional) Whether the datashare is associated with the entire account. Conflicts with `consumer_arn` and `consumer_region`.
* `consumer_arn` - (Optional) Amazon Resource Name (ARN) of the consumer that is associated with the datashare. Conflicts with `associate_entire_account` and `consumer_region`.
* `consumer_region` - (Optional) From a datashare consumer account, associates a datashare with all existing and future namespaces in the specified AWS Region. Conflicts with `associate_entire_account` and `consumer_arn`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - A comma-delimited string concatenating `data_share_arn` and `associate_entire_account`, `consumer_arn`, and `consumer_region`. As only one of the final three arguments can be specified, the other two will always be empty.
* `managed_by` - Identifier of a datashare to show its managing entity.
* `producer_arn` - Amazon Resource Name (ARN) of the producer.

## Import

```bash
ytofu import aws_redshift_data_share_consumer_association.example arn:aws:redshift:us-west-2:123456789012:datashare:b3bfde75-73fd-408b-9086-d6fccfd6d588/example,,,us-west-2
```
