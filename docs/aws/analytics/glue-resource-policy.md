# Glue Resource Policy

Manage Glue Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

data:
  aws_region:
    current:

data:
  aws_iam_policy_document:
    glue-example-policy:
      statement:
        actions:
          - "glue:CreateTable"
        resources: 
          - "arn:${data.aws_partition.current.partition}:glue:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:*"
        principals:
          identifiers: 
            - "*"
          type: AWS

resource:
  aws_glue_resource_policy:
    example:
      policy: ${data.aws_iam_policy_document.glue-example-policy.json}
```
