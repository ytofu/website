# Codecommit Approval Rule Template

Manage Codecommit Approval Rule Template resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codecommit_approval_rule_template:
    example:
      name: MyExampleApprovalRuleTemplate
      description: This is an example approval rule template
      content: '{ "Version": "2018-11-08" "DestinationReferences": ["refs/heads/master"] "Statements": [{ "Type": "Approvers" "NumberOfApprovalsNeeded": 2 "ApprovalPoolMembers": ["arn:aws:sts::123456789012:assumed-role/CodeCommitReview/*"] }] }'
```
