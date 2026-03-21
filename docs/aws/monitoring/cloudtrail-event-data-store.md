# Cloudtrail Event Data Store

Manage Cloudtrail Event Data Store resources using ytofu YAML.

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
