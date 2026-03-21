# Resource: aws_apprunner_custom_domain_association

Manages an App Runner Custom Domain association.

## Basic Example

```yaml
resource:
  aws_apprunner_custom_domain_association:
    example:
      domain_name: example.com
      service_arn: ${aws_apprunner_service.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `domain_name` - (Required) Custom domain endpoint to association. Specify a base domain e.g., `example.com` or a subdomain e.g., `subdomain.example.com`.
* `enable_www_subdomain` (Optional) Whether to associate the subdomain with the App Runner service in addition to the base domain. Defaults to `true`.
* `service_arn` - (Required) ARN of the App Runner service.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The `domain_name` and `service_arn` separated by a comma (`,`).
* `certificate_validation_records` - A set of certificate CNAME records used for this domain name. See [Certificate Validation Records](#certificate-validation-records) below for more details.
* `dns_target` - App Runner subdomain of the App Runner service. The custom domain name is mapped to this target name. Attribute only available if resource created (not imported) with ytofu.

### Certificate Validation Records

The configuration block consists of the following arguments:

* `name` - Certificate CNAME record name.
* `status` - Current state of the certificate CNAME record validation. It should change to `SUCCESS` after App Runner completes validation with your DNS.
* `type` - Record type, always `CNAME`.
* `value` - Certificate CNAME record value.

## Import

```bash
ytofu import aws_apprunner_custom_domain_association.example example.com,arn:aws:apprunner:us-east-1:123456789012:service/example-app/8fe1e10304f84fd2b0df550fe98a71fa
```
