# Resource: aws_grafana_license_association

Provides an Amazon Managed Grafana workspace license association resource.

## Basic Example

```yaml
resource:
  aws_grafana_license_association:
    example:
      license_type: ENTERPRISE_FREE_TRIAL
      workspace_id: ${aws_grafana_workspace.example.id}

  aws_grafana_workspace:
    example:
      account_access_type: CURRENT_ACCOUNT
      authentication_providers: 
        - SAML
      permission_type: SERVICE_MANAGED
      role_arn: ${aws_iam_role.assume.arn}

  aws_iam_role:
    assume:
      name: grafana-assume
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "grafana.amazonaws.com" } }, ] }'```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `grafana_token` - (Optional) A token from Grafana Labs that ties your AWS account with a Grafana Labs account.
* `license_type` - (Required) The type of license for the workspace license association. Valid values are `ENTERPRISE` and `ENTERPRISE_FREE_TRIAL`.
* `workspace_id` - (Required) The workspace id.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `free_trial_expiration` - If `license_type` is set to `ENTERPRISE_FREE_TRIAL`, this is the expiration date of the free trial.
* `license_expiration` - If `license_type` is set to `ENTERPRISE`, this is the expiration date of the enterprise license.

## Import

```bash
ytofu import aws_grafana_license_association.example g-2054c75a02
```
