# Resource: aws_schemas_registry_policy

ytofu resource for managing an AWS EventBridge Schemas Registry Policy.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    example:
      statement:
        sid: example
        effect: Allow
        principals:
          type: AWS
          identifiers:
            - 109876543210
        actions: 
          - "schemas:*"
        resources:
          - "arn:aws:schemas:us-east-1:123456789012:registry/example"
          - "arn:aws:schemas:us-east-1:123456789012:schema/example*"

resource:
  aws_schemas_registry_policy:
    example:
      registry_name: example
      policy: ${data.aws_iam_policy_document.example.json}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `registry_name` - (Required) Name of EventBridge Schema Registry
* `policy` - (Required) Resource Policy for EventBridge Schema Registry

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `update` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_schemas_registry_policy.example example
```
