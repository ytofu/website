# Workspacesweb Session Logger Association

Manage Workspacesweb Session Logger Association resources using ytofu YAML.

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
