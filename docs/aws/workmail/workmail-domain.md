# Resource: aws_workmail_domain

Manages a mail domain registered to an AWS WorkMail organization.

## Basic Example

```yaml
resource:
  aws_workmail_domain:
    example:
      organization_id: ${aws_workmail_organization.example.id}
      domain_name: example.com
```

## Argument Reference

This resource supports the following arguments:

* `domain_name` - (Required) Mail domain name to register. Changing this forces a new resource.
* `organization_id` - (Required) Identifier of the WorkMail organization. Changing this forces a new resource.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `dkim_verification_status` - DKIM verification status. Values: `PENDING`, `VERIFIED`, `FAILED`.
* `is_default` - Whether this domain is the default mail domain for the organization.
* `is_test_domain` - Whether this is the auto-provisioned test domain.
* `ownership_verification_status` - Domain ownership verification status. Values: `PENDING`, `VERIFIED`, `FAILED`.
* `records` - List of DNS records required for domain verification. See [`records`](#records) below.

### `records`

Each `records` block exports the following:

* `hostname` - DNS record hostname.
* `type` - DNS record type (e.g. `CNAME`, `MX`, `TXT`).
* `value` - DNS record value.

## Import

```bash
ytofu import aws_workmail_domain.example "m-1234567890abcdef0,example.com"
```
