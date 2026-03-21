# Config Organization Custom Policy Rule

Manage Config Organization Custom Policy Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_config_organization_custom_policy_rule:
    example:
      name: example_rule_name
      policy_runtime: guard-2.x.x
      policy_text: |
        let status = ['ACTIVE']
        
        rule tableisactive when
        resourceType == "AWS::DynamoDB::Table" {
        configuration.tableStatus == %status
        }
        
        rule checkcompliance when
        resourceType == "AWS::DynamoDB::Table"
        tableisactive {
        let pitr = supplementaryConfiguration.ContinuousBackupsDescription.pointInTimeRecoveryDescription.pointInTimeRecoveryStatus
        %pitr == "ENABLED"
        }
      resource_types_scope: 
        - "AWS::DynamoDB::Table"
```
