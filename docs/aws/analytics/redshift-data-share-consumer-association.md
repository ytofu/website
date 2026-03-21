# Redshift Data Share Consumer Association

Manage Redshift Data Share Consumer Association resources using ytofu YAML.

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
