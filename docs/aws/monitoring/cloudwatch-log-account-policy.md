# Cloudwatch Log Account Policy

Manage Cloudwatch Log Account Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_account_policy:
    data_protection:
      policy_name: data-protection
      policy_type: DATA_PROTECTION_POLICY
      policy_document: '{ "Name": "DataProtection" "Version": "2021-06-01" "Statement": [ { "Sid": "Audit" "DataIdentifier": ["arn:aws:dataprotection::aws:data-identifier/EmailAddress"] "Operation": { "Audit": { "FindingsDestination": {} } } }, { "Sid": "Redact" "DataIdentifier": ["arn:aws:dataprotection::aws:data-identifier/EmailAddress"] "Operation": { "Deidentify": { "MaskConfig": {} } } } ] }'
```

## Subscription Filter Policy

```yaml
resource:
  aws_cloudwatch_log_account_policy:
    subscription_filter:
      policy_name: subscription-filter
      policy_type: SUBSCRIPTION_FILTER_POLICY
      policy_document: 'example-json-policy'
      selection_criteria: LogGroupName NOT IN [\"excluded_log_group_name\"]
```

## Field Index Policy

```yaml
resource:
  aws_cloudwatch_log_account_policy:
    field_index:
      policy_name: field-index
      policy_type: FIELD_INDEX_POLICY
      policy_document: 'example-json-policy'
```
