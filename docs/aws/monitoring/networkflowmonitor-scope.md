# Resource: aws_networkflowmonitor_scope

Manages a Network Flow Monitor Scope.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_networkflowmonitor_scope:
    example:
      target:
        region: us-east-1
        target_identifier:
          target_type: ACCOUNT
          target_id:
            account_id: ${data.aws_caller_identity.current.account_id}
      tags:
        Name: example
```

## Argument Reference

The following arguments are required:

* `target` - (Required) The targets to define the scope to be monitored. A target is an array of target resources, which are currently Region-account pairs.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### targets

The `targets` block supports the following:

* `region` - (Required) The AWS Region for the scope.
* `target_identifier` - (Required) A target identifier is a pair of identifying information for a scope.

### target_identifier

The `target_identifier` block supports the following:

* `target_id` - (Required) The identifier for a target, which is currently always an account ID.
* `target_type` - (Required) The type of a target. A target type is currently always `ACCOUNT`.

### target_id

The `target_id` block supports the following:

* `account_id` - (Required) AWS account ID.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `scope_arn` - The Amazon Resource Name (ARN) of the scope.
* `scope_id` - The identifier for the scope that includes the resources you want to get data results for.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_networkflowmonitor_scope.example example-scope-id
```
