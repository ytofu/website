# Resource: aws_codebuild_resource_policy

Provides a CodeBuild Resource Policy Resource.

## Basic Example

```yaml
resource:
  aws_codebuild_report_group:
    example:
      name: example
      type: TEST
      export_config:
        type: NO_EXPORT

  aws_codebuild_resource_policy:
    example:
      resource_arn: ${aws_codebuild_report_group.example.arn}
      policy: '{ "Version": "2012-10-17" "Id": "default" "Statement": [{ "Sid": "default" "Effect": "Allow" "Principal": { "AWS": "arn:${data.aws_partition.current.partition}:iam::${data.aws_caller_identity.current.account_id}:root" } "Action": [ "codebuild:BatchGetReportGroups", "codebuild:BatchGetReports", "codebuild:ListReportsForReportGroup", "codebuild:DescribeTestCases", ] "Resource": aws_codebuild_report_group.example.arn }] }'

data:
  aws_partition:
    current:

  aws_caller_identity:
    current:```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_arn` - (Required) The ARN of the Project or ReportGroup resource you want to associate with a resource policy.
* `policy` - (Required) A JSON-formatted resource policy. For more information, see [Sharing a Projec](https://docs.aws.amazon.com/codebuild/latest/userguide/project-sharing.html#project-sharing-share) and [Sharing a Report Group](https://docs.aws.amazon.com/codebuild/latest/userguide/report-groups-sharing.html#report-groups-sharing-share).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ARN of Resource.

## Import

```bash
ytofu import aws_codebuild_resource_policy.example arn:aws:codebuild:us-west-2:123456789:report-group/report-group-name
```
