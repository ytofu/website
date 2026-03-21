# Redshift Data Share Authorization

Manage Redshift Data Share Authorization resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_data_share_authorization:
    example:
      consumer_identifier: 123456789012
      data_share_arn: "arn:aws:redshift:us-west-2:123456789012:datashare:3072dae5-022b-4d45-9cd3-01f010aae4b2/example_share"
```
