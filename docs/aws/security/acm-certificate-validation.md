# Resource: aws_acm_certificate_validation

This resource represents a successful validation of an ACM certificate in concert
with other resources.

## Basic Example

```yaml
resource:
  aws_acm_certificate:
    example:
      domain_name: example.com
      validation_method: DNS

  aws_route53_record:
    example:
      allow_overwrite: true
      name: example-resource_record_name
      records:
        - example-resource_record_value
      ttl: 60
      type: example-resource_record_type
      zone_id: ${data.aws_route53_zone.example.zone_id}

  aws_acm_certificate_validation:
    example:
      certificate_arn: ${aws_acm_certificate.example.arn}
      validation_record_fqdns: 'example-list'

  aws_lb_listener:
    example:
      certificate_arn: ${aws_acm_certificate_validation.example.certificate_arn}

data:
  aws_route53_zone:
    example:
      name: example.com
      private_zone: false```

## Alternative Domains DNS Validation with Route 53

```yaml
resource:
  aws_acm_certificate:
    example:
      domain_name: example.com
      subject_alternative_names: 
        - www.example.com
        - example.org
      validation_method: DNS

  aws_route53_record:
    example:
      allow_overwrite: true
      name: example-resource_record_name
      records:
        - example-resource_record_value
      ttl: 60
      type: example-resource_record_type
      zone_id: data.aws_route53_zone.example_org.zone_id

  aws_acm_certificate_validation:
    example:
      certificate_arn: ${aws_acm_certificate.example.arn}
      validation_record_fqdns: 'example-list'

  aws_lb_listener:
    example:
      certificate_arn: ${aws_acm_certificate_validation.example.certificate_arn}

data:
  aws_route53_zone:
    example_com:
      name: example.com
      private_zone: false

  aws_route53_zone:
    example_org:
      name: example.org
      private_zone: false```

## Email Validation

```yaml
resource:
  aws_acm_certificate:
    example:
      domain_name: example.com
      validation_method: EMAIL

  aws_acm_certificate_validation:
    example:
      certificate_arn: ${aws_acm_certificate.example.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `certificate_arn` - (Required) ARN of the certificate that is being validated.
* `validation_record_fqdns` - (Optional) List of FQDNs that implement the validation. Only valid for DNS validation method ACM certificates. If this is set, the resource can implement additional sanity checks and has an explicit dependency on the resource that is implementing the validation

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Time at which the certificate was issued

## Timeouts

Configuration options:

- `create` - (Default `75m`)
