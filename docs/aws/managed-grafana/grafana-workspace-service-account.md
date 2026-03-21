# Resource: aws_grafana_workspace_service_account



## Basic Example

```yaml
resource:
  aws_grafana_workspace_service_account:
    example:
      name: example-admin
      grafana_role: ADMIN
      workspace_id: ${aws_grafana_workspace.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) A name for the service account. The name must be unique within the workspace, as it determines the ID associated with the service account.
* `grafana_role` - (Required) The permission level to use for this service account. For more information about the roles and the permissions each has, see the [User roles](https://docs.aws.amazon.com/grafana/latest/userguide/Grafana-user-roles.html) documentation.
* `workspace_id` - (Required) The Grafana workspace with which the service account is associated.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `service_account_id` - Identifier of the service account in the given Grafana workspace

## Import

```bash
ytofu import aws_grafana_workspace_service_account.example g-abc12345,1
```
