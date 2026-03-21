# Resource: aws_sesv2_tenant_resource_association

Manages an AWS SESv2 (Simple Email V2) Tenant Resource Association.

## Basic Example

```yaml
resource:
  aws_sesv2_tenant_resource_association:
    example:
      tenant_name: example-tenant
      resource_arn: "arn:aws:ses:us-east-1:123456789012:configuration-set/example"
```

## Argument Reference

The following arguments are required:

* `tenant_name` - (Required) Name of SES Tenant.
* `resource_arn` - (Required) ARN of the SES resource to associate with the tenant.

The following arguments are optional:

* `region` - (Optional) AWS region for SESv2 operations. If not specified, the default provider region is used.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_sesv2_tenant_resource_association.example "example-tenant|arn:aws:ses:us-east-1:123456789012:configuration-set/example"
```
