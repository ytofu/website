# Resource: aws_grafana_role_association

Provides an Amazon Managed Grafana workspace role association resource.

## Basic Example

```yaml
resource:
  aws_grafana_role_association:
    example:
      role: ADMIN
      user_ids: 
        - USER_ID_1
        - USER_ID_2
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

## Argument Reference

The following arguments are required:

* `role` - (Required) The grafana role. Valid values can be found [here](https://docs.aws.amazon.com/grafana/latest/APIReference/API_UpdateInstruction.html#ManagedGrafana-Type-UpdateInstruction-role).
* `workspace_id` - (Required) The workspace id.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `group_ids` - (Optional) The AWS SSO group ids to be assigned the role given in `role`.
* `user_ids` - (Optional) The AWS SSO user ids to be assigned the role given in `role`.

## Attribute Reference

This resource exports no additional attributes.
