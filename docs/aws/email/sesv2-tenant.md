# Resource: aws_sesv2_tenant

Manages an AWS SESv2 (Simple Email V2) Tenant.

## Basic Example

```yaml
resource:
  aws_sesv2_tenant:
    example:
      tenant_name: example-tenant
      tags:
        Environment: test
```

## Argument Reference

The following arguments are required:

* `tenant_name` - (Required) Name of the SESV2 tenant.  The name must be unique within the AWS account and Region.  Changing the tenant name forces creation of a new tenant.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Map of tags to assign to the tenant.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `sending_status` – Current sending status of the tenant.
* `tags_all` – Map of tags assigned to the tenant, including provider default tags.
* `tenant_arn` - ARN of the Tenant.
* `tenant_id` - ID of the Tenant.

## Import

```bash
ytofu import aws_sesv2_tenant.example example-tenant
```
