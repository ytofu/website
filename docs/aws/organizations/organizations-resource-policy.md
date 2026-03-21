# Organizations Resource Policy

Manage Organizations Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_organizations_resource_policy:
    example:
      content: |
        {
        "Version": "2012-10-17",
        "Statement": [
        {
        "Sid": "DelegatingNecessaryDescribeListActions",
        "Effect": "Allow",
        "Principal": {
        "AWS": "arn:aws:iam::123456789012:root"
        },
        "Action": [
        "organizations:DescribeOrganization",
        "organizations:DescribeOrganizationalUnit",
        "organizations:DescribeAccount",
        "organizations:DescribePolicy",
        "organizations:DescribeEffectivePolicy",
        "organizations:ListRoots",
        "organizations:ListOrganizationalUnitsForParent",
        "organizations:ListParents",
        "organizations:ListChildren",
        "organizations:ListAccounts",
        "organizations:ListAccountsForParent",
        "organizations:ListPolicies",
        "organizations:ListPoliciesForTarget",
        "organizations:ListTargetsForPolicy",
        "organizations:ListTagsForResource"
        ],
        "Resource": "*"
        }
        ]
        }
```
