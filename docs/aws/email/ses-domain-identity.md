# Resource: aws_ses_domain_identity

Provides an SES domain identity resource

## Basic Example

```yaml
resource:
  aws_ses_domain_identity:
    example:
      domain: example.com
```

## With Route53 Record

```yaml
resource:
  aws_ses_domain_identity:
    example:
      domain: example.com

  aws_route53_record:
    example_amazonses_verification_record:
      zone_id: ABCDEFGHIJ123
      name: _amazonses.example.com
      type: TXT
      ttl: 600
      records: 
        - ${aws_ses_domain_identity.example.verification_token}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `domain` - (Required) The domain name to assign to SES

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the domain identity.
* `verification_token` - A code which when added to the domain as a TXT record will signal to SES that the owner of the domain has authorized SES to act on their behalf. The domain identity will be in state "verification pending" until this is done. See the [With Route53 Record](#with-route53-record) example for how this might be achieved when the domain is hosted in Route 53 and managed by ytofu.  Find out more about verifying domains in Amazon SES in the [AWS SES docs](http://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-domains.html).

## Import

```bash
ytofu import aws_ses_domain_identity.example example.com
```
