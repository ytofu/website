# Resource: aws_workspacesweb_session_logger_association

ytofu resource for managing an AWS WorkSpaces Web Session Logger Association.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

resource:
  aws_s3_bucket:
    example:
      bucket: example-session-logs
      force_destroy: true

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - workspaces-web.amazonaws.com
        actions:
          - "s3:PutObject"
        resources:
          - "${aws_s3_bucket.example.arn}/*"

resource:
  aws_s3_bucket_policy:
    example:
      bucket: ${aws_s3_bucket.example.id}
      policy: ${data.aws_iam_policy_document.example.json}

resource:
  aws_workspacesweb_session_logger:
    example:
      display_name: example
      event_filter:
        all: {}
      log_configuration:
        s3:
          bucket: ${aws_s3_bucket.example.id}
          folder_structure: Flat
          log_file_format: Json
      depends_on: 
        - ${aws_s3_bucket_policy.example}

resource:
  aws_workspacesweb_session_logger_association:
    example:
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}
      session_logger_arn: ${aws_workspacesweb_session_logger.example.session_logger_arn}
```

## Argument Reference

The following arguments are required:

* `portal_arn` - (Required) ARN of the web portal.
* `session_logger_arn` - (Required) ARN of the session logger.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_workspacesweb_session_logger_association.example arn:aws:workspaces-web:us-west-2:123456789012:sessionLogger/session_logger-id-12345678,arn:aws:workspaces-web:us-west-2:123456789012:portal/portal-id-12345678
```
