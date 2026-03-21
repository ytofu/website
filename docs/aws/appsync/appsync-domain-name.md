# Resource: aws_appsync_domain_name

Provides an AppSync Domain Name.

## Basic Example

```yaml
resource:
  aws_appsync_domain_name:
    example:
      domain_name: api.example.com
      certificate_arn: ${aws_acm_certificate.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `certificate_arn` - (Required) ARN of the certificate. This can be an Certificate Manager (ACM) certificate or an Identity and Access Management (IAM) server certificate. The certifiacte must reside in us-east-1.
* `description` - (Optional)  A description of the Domain Name.
* `domain_name` - (Required) Domain name.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Appsync Domain Name.
* `appsync_domain_name` - Domain name that AppSync provides.
* `hosted_zone_id` - ID of your Amazon Route 53 hosted zone.

## Import

```bash
ytofu import aws_appsync_domain_name.example example.com
```
