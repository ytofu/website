# Resource: aws_observabilityadmin_telemetry_pipeline

Manages an AWS CloudWatch Observability Admin Telemetry Pipeline.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

  aws_partition:
    current:

resource:
  aws_iam_role:
    example:
      name: example-telemetry-pipeline
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [{ "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "observabilityadmin.amazonaws.com" } }] }'

  aws_iam_role_policy:
    example:
      role: ${aws_iam_role.example.name}
      policy: '{ "Version": "2012-10-17" "Statement": [{ "Effect": "Allow" "Action": [ "logs:CreateLogGroup", "logs:CreateLogStream", "logs:PutLogEvents", "logs:DescribeLogGroups", "logs:DescribeLogStreams", ] "Resource": "arn:${data.aws_partition.current.partition}:logs:*:${data.aws_caller_identity.current.account_id}:*" }] }'

  aws_observabilityadmin_telemetry_pipeline:
    example:
      name: example-pipeline
      configuration:
        body: '# yamlencode content'
      depends_on:
        - ${aws_iam_role_policy.example}```

## Pipeline with Processor

```yaml
resource:
  aws_observabilityadmin_telemetry_pipeline:
    example:
      name: example-vpc-pipeline
      configuration:
        body: '# yamlencode content'
      depends_on: 
        - ${aws_iam_role_policy.example}
```

## Argument Reference

This resource supports the following arguments:

* `name` - (Required, Forces new resource) Name of the telemetry pipeline. Must be between 3 and 28 characters, start with a lowercase letter, and contain only lowercase letters, digits, and hyphens.
* `configuration` - (Required) Configuration block for the telemetry pipeline. See [`configuration`](#configuration) below.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### configuration

* `body` - (Required) The pipeline configuration body. This is a YAML-encoded string defining the pipeline source, optional processors, and sinks.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the telemetry pipeline.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `30m`)
- `update` - (Default `30m`)
- `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_observabilityadmin_telemetry_pipeline.example arn:aws:observabilityadmin:us-west-2:1234567890:telemetry-pipeline/id
```
