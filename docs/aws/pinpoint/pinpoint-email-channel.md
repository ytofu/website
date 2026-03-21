# Pinpoint Email Channel

Manage Pinpoint Email Channel resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_pinpoint_email_channel:
    email:
      application_id: ${aws_pinpoint_app.app.application_id}
      from_address: user@example.com
      role_arn: ${aws_iam_role.role.arn}

resource:
  aws_pinpoint_app:
    app:

resource:
  aws_ses_domain_identity:
    identity:
      domain: example.com

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - pinpoint.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    role:
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    role_policy:
      statement:
        effect: Allow
        actions:
          - "mobileanalytics:PutEvents"
          - "mobileanalytics:PutItems"
        resources: 
          - "*"

resource:
  aws_iam_role_policy:
    role_policy:
      name: role_policy
      role: ${aws_iam_role.role.id}
      policy: ${data.aws_iam_policy_document.role_policy.json}
```
