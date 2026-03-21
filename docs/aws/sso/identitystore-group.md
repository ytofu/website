# Resource: aws_identitystore_group

ytofu resource for managing an AWS IdentityStore Group.

## Basic Example

```yaml
resource:
  aws_identitystore_group:
    this:
      display_name: Example group
      description: Example description
      identity_store_id: ${data.aws_ssoadmin_instances.example.identity_store_ids[0]}
```

## Argument Reference

The following arguments are required:

* `identity_store_id` - (Required) The globally unique identifier for the identity store.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `display_name` - (Optional) A string containing the name of the group. This value is commonly displayed when the group is referenced.
* `description` - (Optional) A string containing the description of the group.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Group.
* `group_id` - The identifier of the newly created group in the identity store.
* `external_ids` - A list of external IDs that contains the identifiers issued to this resource by an external identity provider. See [External IDs](#external-ids) below.

### External IDs

* `id` - The identifier issued to this resource by an external identity provider.
* `issuer` - The issuer for an external identifier.

## Timeouts

Configuration options:

* `create` - (Default `60m`)
* `update` - (Default `180m`)
* `delete` - (Default `90m`)

## Import

```bash
ytofu import aws_identitystore_group.example d-9c6705e95c/b8a1c340-8031-7071-a2fb-7dc540320c30
```
