# Resource: aws_workspacesweb_trust_store_association

ytofu resource for managing an AWS WorkSpaces Web Trust Store Association.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

  aws_workspacesweb_trust_store:
    example:
      certificate_list: 
        - example-value

  aws_workspacesweb_trust_store_association:
    example:
      trust_store_arn: ${aws_workspacesweb_trust_store.example.trust_store_arn}
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}```

## Argument Reference

The following arguments are required:

* `trust_store_arn` - (Required) ARN of the trust store to associate with the portal. Forces replacement if changed.
* `portal_arn` - (Required) ARN of the portal to associate with the trust store. Forces replacement if changed.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_workspacesweb_trust_store_association.example arn:aws:workspaces-web:us-west-2:123456789012:trustStore/trust_store-id-12345678,arn:aws:workspaces-web:us-west-2:123456789012:portal/portal-id-12345678
```
