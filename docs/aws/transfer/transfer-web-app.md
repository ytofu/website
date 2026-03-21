# Transfer Web App

Manage Transfer Web App resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_region:
    current:

data:
  aws_partition:
    current:

data:
  aws_ssoadmin_instances:
    example:

data:
  aws_iam_policy_document:
    assume_role_transfer:
      statement:
        effect: Allow
        actions:
          - "sts:AssumeRole"
          - "sts:SetContext"
        principals:
          type: Service
          identifiers: 
            - transfer.amazonaws.com
        condition:
          test: StringEquals
          values: 
            - ${data.aws_caller_identity.current.account_id}

resource:
  aws_iam_role:
    example:
      name: example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role_transfer.json}

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        actions:
          - "s3:GetDataAccess"
          - "s3:ListCallerAccessGrants"
        resources:
          - "arn:${data.aws_partition.current.partition}:s3:${data.aws_region.current.name}:${data.aws_caller_identity.current.account_id}:access-grants/*"
        condition:
          test: StringEquals
          values: 
            - ${data.aws_caller_identity.current.account_id}
      statement:
        effect: Allow
        actions:
          - "s3:ListAccessGrantsInstances"
        resources: 
          - "*"
        condition:
          test: StringEquals
          values: 
            - ${data.aws_caller_identity.current.account_id}

resource:
  aws_iam_role_policy:
    example:
      policy: ${data.aws_iam_policy_document.example.json}
      role: ${aws_iam_role.example.name}

resource:
  aws_transfer_web_app:
    example:
      identity_provider_details:
        identity_center_config:
          instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
          role: ${aws_iam_role.example.arn}
      web_app_units:
        provisioned: 1
      tags:
        Name: test
```
