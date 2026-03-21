# Resource: aws_ses_domain_identity_verification

Represents a successful verification of an SES domain identity.

## Basic Example

```yaml
resource:
  aws_ses_domain_identity:
    example:
      domain: example.com

  aws_route53_record:
    example_amazonses_verification_record:
      zone_id: ${aws_route53_zone.example.zone_id}
      name: "_amazonses.${aws_ses_domain_identity.example.domain}"
      type: TXT
      ttl: 600
      records: 
        - ${aws_ses_domain_identity.example.verification_token}

  aws_ses_domain_identity_verification:
    example_verification:
      domain: ${aws_ses_domain_identity.example.domain}
      depends_on: 
        - ${aws_route53_record.example_amazonses_verification_record}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `domain` - (Required) The domain name of the SES domain identity to verify.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The domain name of the domain identity.
* `arn` - The ARN of the domain identity.

## Timeouts

Configuration options:

- `create` - (Default `45m`)
