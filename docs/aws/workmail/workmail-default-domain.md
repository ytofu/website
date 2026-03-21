# Resource: aws_workmail_default_domain

Manages the default mail domain for an AWS WorkMail organization.

## Basic Example

```yaml
resource:
  aws_workmail_organization:
    example:
      organization_alias: example-org

  aws_workmail_default_domain:
    example:
      organization_id: ${aws_workmail_organization.example.id}
      domain_name: ${aws_workmail_organization.example.default_mail_domain}```

## Argument Reference

This resource supports the following arguments:

* `domain_name` - (Required) Mail domain name to set as the default.
* `organization_id` - (Required) Identifier of the WorkMail organization. Changing this forces a new resource.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_workmail_default_domain.example "m-1234567890abcdef0"
```
