# Resource: aws_verifiedpermissions_schema

This is a ytofu resource for managing an AWS Verified Permissions Policy Store Schema.

## Basic Example

```yaml
resource:
  aws_verifiedpermissions_schema:
    example:
      policy_store_id: ${aws_verifiedpermissions_policy_store.example.policy_store_id}
      definition:
        value: '{ "Namespace" : { "entityTypes" : {}, "actions" : {} } }'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `policy_store_id` - (Required) The ID of the Policy Store.
* `definition` - (Required) The definition of the schema.
    * `value` - (Required) A JSON string representation of the schema.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `namespaces` - (Optional) Identifies the namespaces of the entities referenced by this schema.

## Import

```bash
ytofu import aws_verifiedpermissions_schema.example DxQg2j8xvXJQ1tQCYNWj9T
```
