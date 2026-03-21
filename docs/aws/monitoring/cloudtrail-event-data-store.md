# Resource: aws_cloudtrail_event_data_store

Provides a CloudTrail Event Data Store.

## Basic Example

```yaml
resource:
  aws_cloudtrail_event_data_store:
    example:
      name: example-event-data-store
```

## Data Event Logging

```yaml
data:
  aws_dynamodb_table:
    table:
      name: not-important-dynamodb-table

resource:
  aws_cloudtrail_event_data_store:
    example:
      advanced_event_selector:
        name: Log all DynamoDB PutEvent actions for a specific DynamoDB table
        field_selector:
          field: eventCategory
          equals: 
            - Data
        field_selector:
          field: resources.type
          equals:
            - "AWS::DynamoDB::Table"
        field_selector:
          field: eventName
          equals: 
            - PutItem
        field_selector:
          field: resources.ARN
          equals:
            - ${data.aws_dynamodb_table.table.arn}
```

## Argument Reference

This resource supports the following arguments:

- `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
- `name` - (Required) The name of the event data store.
- `billing_mode` - (Optional) The billing mode for the event data store. The valid values are `EXTENDABLE_RETENTION_PRICING` and `FIXED_RETENTION_PRICING`. Defaults to `EXTENDABLE_RETENTION_PRICING`.
- `suspend` - (Optional) Specifies whether to stop ingesting new events into the event data store. If set to `true`, ingestion is suspended while maintaining the ability to query existing events. If set to `false`, ingestion is active.
- `advanced_event_selector` - (Optional) The advanced event selectors to use to select the events for the data store. For more information about how to use advanced event selectors, see [Log events by using advanced event selectors](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/logging-data-events-with-cloudtrail.html#creating-data-event-selectors-advanced) in the CloudTrail User Guide.
- `multi_region_enabled` - (Optional) Specifies whether the event data store includes events from all regions, or only from the region in which the event data store is created. Default: `true`.
- `organization_enabled` - (Optional) Specifies whether an event data store collects events logged for an organization in AWS Organizations. Default: `false`.
- `retention_period` - (Optional) The retention period of the event data store, in days. You can set a retention period of up to 2555 days, the equivalent of seven years. Default: `2555`.
- `kms_key_id` - Specifies the AWS KMS key ID to use to encrypt the events delivered by CloudTrail. The value can be an alias name prefixed by alias/, a fully specified ARN to an alias, a fully specified ARN to a key, or a globally unique identifier.
- `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
- `termination_protection_enabled` - (Optional) Specifies whether termination protection is enabled for the event data store. If termination protection is enabled, you cannot delete the event data store until termination protection is disabled. Default: `true`.

### Advanced Event Selector Arguments

`advanced_event_selector` supports the following arguments:

- `name` (Optional) - Specifies the name of the advanced event selector.
- `field_selector` (Required) - Specifies the selector statements in an advanced event selector. Fields documented below.

#### Field Selector Arguments

`field_selector` supports the following arguments:

- `field` (Required) - Specifies a field in an event record on which to filter events to be logged. You can specify only the following values: `readOnly`, `eventSource`, `eventName`, `eventCategory`, `resources.type`, `resources.ARN`.
- `equals` (Optional) - A list of values that includes events that match the exact value of the event record field specified as the value of `field`. This is the only valid operator that you can use with the `readOnly`, `eventCategory`, and `resources.type` fields.
- `not_equals` (Optional) - A list of values that excludes events that match the exact value of the event record field specified as the value of `field`.
- `starts_with` (Optional) - A list of values that includes events that match the first few characters of the event record field specified as the value of `field`.
- `not_starts_with` (Optional) - A list of values that excludes events that match the first few characters of the event record field specified as the value of `field`.
- `ends_with` (Optional) - A list of values that includes events that match the last few characters of the event record field specified as the value of `field`.
- `not_ends_with` (Optional) - A list of values that excludes events that match the last few characters of the event record field specified as the value of `field`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

- `arn` - ARN of the event data store.
- `id` - Name of the event data store.
- `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_cloudtrail_event_data_store.example arn:aws:cloudtrail:us-east-1:123456789123:eventdatastore/22333815-4414-412c-b155-dd254033gfhf
```
