# Codebuild Resource Policy

Manage Codebuild Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codebuild_report_group:
    example:
      name: example
      type: TEST
      export_config:
        type: NO_EXPORT

data:
  aws_partition:
    current:

data:
  aws_caller_identity:
    current:

resource:
  aws_codebuild_resource_policy:
    example:
      resource_arn: ${aws_codebuild_report_group.example.arn}
      policy: '{ "Version": "2012-10-17" "Id": "default" "Statement": [{ "Sid": "default" "Effect": "Allow" "Principal": { "AWS": "arn:${data.aws_partition.current.partition}:iam::${data.aws_caller_identity.current.account_id}:root" } "Action": [ "codebuild:BatchGetReportGroups", "codebuild:BatchGetReports", "codebuild:ListReportsForReportGroup", "codebuild:DescribeTestCases", ] "Resource": aws_codebuild_report_group.example.arn }] }'
```
