# Resource: aws_auditmanager_assessment_report

ytofu resource for managing an AWS Audit Manager Assessment Report.

## Basic Example

```yaml
resource:
  aws_auditmanager_assessment_report:
    test:
      name: example
      assessment_id: ${aws_auditmanager_assessment.test.id}
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the assessment report.
* `assessment_id` - (Required) Unique identifier of the assessment to create the report from.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the assessment report.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `author` - Name of the user who created the assessment report.
* `id` - Unique identifier for the assessment report.
* `status` - Current status of the specified assessment report. Valid values are `COMPLETE`, `IN_PROGRESS`, and `FAILED`.

## Import

```bash
ytofu import aws_auditmanager_assessment_report.example abc123-de45
```
