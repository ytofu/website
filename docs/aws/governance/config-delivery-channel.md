# Config Delivery Channel

Manage Config Delivery Channel resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_config_delivery_channel:
    foo:
      name: example
      s3_bucket_name: ${aws_s3_bucket.b.bucket}
      depends_on: 
        - ${aws_config_configuration_recorder.foo}

resource:
  aws_s3_bucket:
    b:
      bucket: example-awsconfig
      force_destroy: true

resource:
  aws_config_configuration_recorder:
    foo:
      name: example
      role_arn: ${aws_iam_role.r.arn}

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - config.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    r:
      name: awsconfig-example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    p:
      statement:
        effect: Allow
        actions: 
          - "s3:*"
        resources:
          - ${aws_s3_bucket.b.arn}
          - "${aws_s3_bucket.b.arn}/*"

resource:
  aws_iam_role_policy:
    p:
      name: awsconfig-example
      role: ${aws_iam_role.r.id}
      policy: ${data.aws_iam_policy_document.p.json}
```
