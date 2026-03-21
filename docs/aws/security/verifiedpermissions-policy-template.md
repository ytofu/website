# Resource: aws_verifiedpermissions_policy_template

ytofu resource for managing an AWS Verified Permissions Policy Template.

## Basic Example

```yaml
resource:
  aws_verifiedpermissions_policy_template:
    example:
      policy_store_id: ${aws_verifiedpermissions_policy_store.example.id}
      statement: "permit (principal in ?principal, action in PhotoFlash::Action::\"FullPhotoAccess\", resource == ?resource) unless { resource.IsPrivate };"
```

## Argument Reference

The following arguments are required:

* `policy_store_id` - (Required) The ID of the Policy Store.
* `statement` - (Required) Defines the content of the statement, written in Cedar policy language.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Provides a description for the policy template.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `policy_template_id` - The ID of the Policy Store.
* `created_date` - The date the Policy Store was created.

## Import

```bash
ytofu import aws_verifiedpermissions_policy_template.example policyStoreId:policyTemplateId
```
