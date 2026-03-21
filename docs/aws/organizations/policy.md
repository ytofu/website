# Organizations Policy

Create organization policies (SCPs, tag policies) using ytofu YAML.

## Service Control Policy

```yaml
resource:
  aws_organizations_policy:
    deny_regions:
      name: deny-non-approved-regions
      description: Deny access to non-approved regions
      content: |
        {
          "Version": "2012-10-17",
          "Statement": [
            {
              "Sid": "DenyNonApprovedRegions",
              "Effect": "Deny",
              "NotAction": [
                "iam:*",
                "organizations:*",
                "sts:*",
                "support:*"
              ],
              "Resource": "*",
              "Condition": {
                "StringNotEquals": {
                  "aws:RequestedRegion": ["us-east-1", "us-west-2", "eu-west-1"]
                }
              }
            }
          ]
        }
```

## Tag Policy

```yaml
resource:
  aws_organizations_policy:
    tag:
      name: tag-policy
      type: TAG_POLICY
      content: |
        {
          "tags": {
            "Environment": {
              "tag_key": {"@@assign": "Environment"},
              "tag_value": {"@@assign": ["Production", "Staging", "Development"]}
            }
          }
        }
```
