# Resource: aws_organizations_tag

Manages an individual Organizations resource tag. This resource should only be used in cases where Organizations resources are created outside ytofu (e.g., Organizations Accounts implicitly created by AWS Control Tower).

## Basic Example

```yaml
data:
  aws_organizations_organization:
    example:

resource:
  aws_organizations_organizational_unit:
    example:
      name: ExampleOU
      parent_id: ${data.aws_organizations_organization.example.roots[0].id}
      lifecycle:
        ignore_changes: 
          - tags

resource:
  aws_organizations_tag:
    example:
      resource_id: ${aws_organizations_organizational_unit.example.id}
      key: ExampleKey
      value: ExampleValue
```

## Argument Reference

This resource supports the following arguments:

* `resource_id` - (Required) Id of the Organizations resource to tag.
* `key` - (Required) Tag name.
* `value` - (Required) Tag value.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Organizations resource identifier and key, separated by a comma (`,`)

## Import

```bash
ytofu import aws_organizations_tag.example ou-1234567,ExampleKey
```
