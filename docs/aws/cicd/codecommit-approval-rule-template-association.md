# Resource: aws_codecommit_approval_rule_template_association

Associates a CodeCommit Approval Rule Template with a Repository.

## Basic Example

```yaml
resource:
  aws_codecommit_approval_rule_template_association:
    example:
      approval_rule_template_name: ${aws_codecommit_approval_rule_template.example.name}
      repository_name: ${aws_codecommit_repository.example.repository_name}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `approval_rule_template_name` - (Required) The name for the approval rule template.
* `repository_name` - (Required) The name of the repository that you want to associate with the template.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the approval rule template and name of the repository, separated by a comma (`,`).

## Import

```bash
ytofu import aws_codecommit_approval_rule_template_association.example approver-rule-for-example,MyExampleRepo
```
