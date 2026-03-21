# Accessanalyzer Analyzer

Manage Accessanalyzer Analyzer resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_accessanalyzer_analyzer:
    example:
      analyzer_name: example
```

## Organization Analyzer

```yaml
resource:
  aws_organizations_organization:
    example:
      aws_service_access_principals: 
        - access-analyzer.amazonaws.com

resource:
  aws_accessanalyzer_analyzer:
    example:
      depends_on: 
        - ${aws_organizations_organization.example}
      analyzer_name: example
      type: ORGANIZATION
```

## Organization Unused Access Analyzer With Analysis Rule

```yaml
resource:
  aws_accessanalyzer_analyzer:
    example:
      analyzer_name: example
      type: ORGANIZATION_UNUSED_ACCESS
      configuration:
        unused_access:
          unused_access_age: 180
          analysis_rule:
            exclusion:
              account_ids:
                - 123456789012
                - 234567890123
            exclusion:
              resource_tags:
                - key1: value1
                - key2: value2
```

## Account Internal Access Analyzer by Resource Types

```yaml
resource:
  aws_accessanalyzer_analyzer:
    test:
      analyzer_name: example
      type: ORGANIZATION_INTERNAL_ACCESS
      configuration:
        internal_access:
          analysis_rule:
            inclusion:
              resource_types:
                - "AWS::S3::Bucket"
                - "AWS::RDS::DBSnapshot"
                - "AWS::DynamoDB::Table"
```

## Organization Internal Access Analyzer by Account ID and Resource ARN

```yaml
resource:
  aws_accessanalyzer_analyzer:
    test:
      analyzer_name: example
      type: ORGANIZATION_INTERNAL_ACCESS
      configuration:
        internal_access:
          analysis_rule:
            inclusion:
              account_ids: 
                - 123456789012
              resource_arns: 
                - "arn:aws:s3:::my-example-bucket"
```
