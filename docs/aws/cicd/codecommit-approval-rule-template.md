# Resource: aws_codecommit_approval_rule_template

Provides a CodeCommit Approval Rule Template Resource.

## Basic Example

```yaml
resource:
  aws_codecommit_approval_rule_template:
    example:
      name: MyExampleApprovalRuleTemplate
      description: This is an example approval rule template
      content: '{ "Version": "2018-11-08" "DestinationReferences": ["refs/heads/master"] "Statements": [{ "Type": "Approvers" "NumberOfApprovalsNeeded": 2 "ApprovalPoolMembers": ["arn:aws:sts::123456789012:assumed-role/CodeCommitReview/*"] }] }'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `content` - (Required) The content of the approval rule template. Maximum of 3000 characters.
* `name` - (Required) The name for the approval rule template. Maximum of 100 characters.
* `description` - (Optional) The description of the approval rule template. Maximum of 1000 characters.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `approval_rule_template_id` - The ID of the approval rule template
* `creation_date` - The date the approval rule template was created, in [RFC3339 format](https://tools.ietf.org/html/rfc3339#section-5.8).
* `last_modified_date` - The date the approval rule template was most recently changed, in [RFC3339 format](https://tools.ietf.org/html/rfc3339#section-5.8).
* `last_modified_user` - The Amazon Resource Name (ARN) of the user who made the most recent changes to the approval rule template.
* `rule_content_sha256` - The SHA-256 hash signature for the content of the approval rule template.

## Import

```bash
ytofu import aws_codecommit_approval_rule_template.imported ExistingApprovalRuleTemplateName
```
