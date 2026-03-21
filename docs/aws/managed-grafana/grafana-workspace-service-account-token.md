# Resource: aws_grafana_workspace_service_account_token



## Basic Example

```yaml
resource:
  aws_grafana_workspace_service_account:
    example:
      name: example-admin
      grafana_role: ADMIN
      workspace_id: ${aws_grafana_workspace.example.id}

  aws_grafana_workspace_service_account_token:
    example:
      name: example-key
      service_account_id: ${aws_grafana_workspace_service_account.example.service_account_id}
      seconds_to_live: 3600
      workspace_id: ${aws_grafana_workspace.example.id}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) A name for the token to create. The name must be unique within the workspace.
* `seconds_to_live` - (Required) Sets how long the token will be valid, in seconds. You can set the time up to 30 days in the future.
* `service_account_id` - (Required) The ID of the service account for which to create a token.
* `workspace_id` - (Required) The Grafana workspace with which the service account token is associated.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `service_account_token_id` - Identifier of the service account token in the given Grafana workspace.
* `created_at` - Specifies when the service account token was created.
* `expires_at` - Specifies when the service account token will expire.
* `key` - The key for the service account token. Used when making calls to the Grafana HTTP APIs to authenticate and authorize the requests.
