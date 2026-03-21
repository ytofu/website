# Sagemaker Feature Group

Manage Sagemaker Feature Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_feature_group:
    example:
      feature_group_name: example
      record_identifier_feature_name: example
      event_time_feature_name: example
      role_arn: ${aws_iam_role.test.arn}
      feature_definition:
        feature_name: example
        feature_type: String
      online_store_config:
        enable_online_store: true
```
