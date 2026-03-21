# Config Configuration Aggregator

Manage Config Configuration Aggregator resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_config_configuration_aggregator:
    account:
      name: example
      account_aggregation_source:
        account_ids: 
          - 123456789012
        regions: 
          - us-west-2
```

## Organization Based Aggregation

```yaml
resource:
  aws_config_configuration_aggregator:
    organization:
      depends_on: 
        - ${aws_iam_role_policy_attachment.organization}
      name: "example" # Required
      organization_aggregation_source:
        all_regions: true
        role_arn: ${aws_iam_role.organization.arn}

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - config.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    organization:
      name: example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_iam_role_policy_attachment:
    organization:
      role: ${aws_iam_role.organization.name}
      policy_arn: "arn:aws:iam::aws:policy/service-role/AWSConfigRoleForOrganizations"
```
