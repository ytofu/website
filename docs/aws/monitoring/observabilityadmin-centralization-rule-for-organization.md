# Observabilityadmin Centralization Rule For Organization

Manage Observabilityadmin Centralization Rule For Organization resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_organizations_organization:
    current:

resource:
  aws_observabilityadmin_centralization_rule_for_organization:
    example:
      rule_name: example-centralization-rule
      rule:
        destination:
          region: eu-west-1
          account: ${data.aws_caller_identity.current.account_id}
        source:
          regions: 
            - ap-southeast-1
          scope: "OrganizationId = '${data.aws_organizations_organization.current.id}'"
          source_logs_configuration:
            encrypted_log_group_strategy: SKIP
            log_group_selection_criteria: "*"
      tags:
        Name: example-centralization-rule
        Environment: production
```

## Advanced Configuration with Encryption, Backup and Log Group Name Configuration

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_organizations_organization:
    current:

resource:
  aws_observabilityadmin_centralization_rule_for_organization:
    advanced:
      rule_name: advanced-centralization-rule
      rule:
        destination:
          region: eu-west-1
          account: ${data.aws_caller_identity.current.account_id}
          destination_logs_configuration:
            logs_encryption_configuration:
              encryption_strategy: AWS_OWNED
            backup_configuration:
              region: us-west-1
            log_group_name_configuration:
              log_group_name_pattern: "/centralized-logs/$${source.accountId}/$${source.region}/$${source.logGroup}"
        source:
          regions: 
            - ap-southeast-1
            - us-east-1
          scope: "OrganizationId = '${data.aws_organizations_organization.current.id}'"
          source_logs_configuration:
            encrypted_log_group_strategy: ALLOW
            log_group_selection_criteria: "*"
      tags:
        Name: advanced-centralization-rule
        Environment: production
        Team: observability
```

## Selective Log Group Filtering

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_organizations_organization:
    current:

resource:
  aws_observabilityadmin_centralization_rule_for_organization:
    filtered:
      rule_name: filtered-centralization-rule
      rule:
        destination:
          region: eu-west-1
          account: ${data.aws_caller_identity.current.account_id}
        source:
          regions: 
            - ap-southeast-1
            - us-east-1
          scope: "OrganizationId = '${data.aws_organizations_organization.current.id}'"
          source_logs_configuration:
            encrypted_log_group_strategy: ALLOW
            log_group_selection_criteria: "LogGroupName LIKE '/aws/lambda%'"
      tags:
        Name: filtered-centralization-rule
        Filter: lambda-logs
```
