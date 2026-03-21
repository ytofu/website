# Resource: aws_redshiftserverless_custom_domain_association

ytofu resource for managing an AWS Redshift Serverless Custom Domain Association.

## Basic Example

```yaml
resource:
  aws_acm_certificate:
    example:
      domain_name: example.com

  aws_redshiftserverless_namespace:
    example:
      namespace_name: example-namespace

  aws_redshiftserverless_workgroup:
    example:
      workgroup_name: example-workgroup
      namespace_name: ${aws_redshiftserverless_namespace.example.namespace_name}

  aws_redshiftserverless_custom_domain_association:
    example:
      workgroup_name: ${aws_redshiftserverless_workgroup.example.workgroup_name}
      custom_domain_name: example.com
      custom_domain_certificate_arn: ${aws_acm_certificate.example.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `workgroup_name` - (Required) Name of the workgroup.
* `custom_domain_name` - (Required) Custom domain to associate with the workgroup.
* `custom_domain_certificate_arn` - (Required) ARN of the certificate for the custom domain association.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `custom_domain_certificate_expiry_time` - Expiration time for the certificate.

## Import

```bash
ytofu import aws_redshiftserverless_custom_domain_association.example example-workgroup,example.com
```
