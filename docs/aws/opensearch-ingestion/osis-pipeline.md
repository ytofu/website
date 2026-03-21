# Osis Pipeline

Manage Osis Pipeline resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_region:
    current:

resource:
  aws_iam_role:
    example:
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "osis-pipelines.amazonaws.com" } }, ] }'

resource:
  aws_osis_pipeline:
    example:
      pipeline_name: example
      pipeline_configuration_body: |
        version: "2"
        example-pipeline:
        source:
        http:
        path: "/example"
        sink:
        - s3:
        aws:
        sts_role_arn: "${aws_iam_role.example.arn}"
        region: "${data.aws_region.current.region}"
        bucket: "example"
        threshold:
        event_collect_timeout: "60s"
        codec:
        ndjson:
      max_units: 1
      min_units: 1
```

## Using file function

```yaml
resource:
  aws_osis_pipeline:
    example:
      pipeline_name: example
      pipeline_configuration_body: file-content
      max_units: 1
      min_units: 1
```
