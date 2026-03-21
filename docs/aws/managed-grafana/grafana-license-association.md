# Grafana License Association

Manage Grafana License Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_grafana_license_association:
    example:
      license_type: ENTERPRISE_FREE_TRIAL
      workspace_id: ${aws_grafana_workspace.example.id}

resource:
  aws_grafana_workspace:
    example:
      account_access_type: CURRENT_ACCOUNT
      authentication_providers: 
        - SAML
      permission_type: SERVICE_MANAGED
      role_arn: ${aws_iam_role.assume.arn}

resource:
  aws_iam_role:
    assume:
      name: grafana-assume
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "grafana.amazonaws.com" } }, ] }'
```
