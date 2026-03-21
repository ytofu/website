# ACM Certificate Validation

Manage ACM Certificate Validation resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_acm_certificate:
    example:
      domain_name: example.com
      validation_method: DNS

data:
  aws_route53_zone:
    example:
      name: example.com
      private_zone: false

resource:
  aws_route53_record:
    example:
      allow_overwrite: true
      name: example-resource_record_name
      records:
        - example-resource_record_value
      ttl: 60
      type: example-resource_record_type
      zone_id: ${data.aws_route53_zone.example.zone_id}

resource:
  aws_acm_certificate_validation:
    example:
      certificate_arn: ${aws_acm_certificate.example.arn}
      validation_record_fqdns: 'example-list'

resource:
  aws_lb_listener:
    example:
      certificate_arn: ${aws_acm_certificate_validation.example.certificate_arn}
```

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

data:
  aws_route53_zone:
    example_com:
      name: example.com
      private_zone: false

data:
  aws_route53_zone:
    example_org:
      name: example.org
      private_zone: false

resource:
  aws_route53_record:
    example:
      allow_overwrite: true
      name: example-resource_record_name
      records:
        - example-resource_record_value
      ttl: 60
      type: example-resource_record_type
      zone_id: data.aws_route53_zone.example_org.zone_id

resource:
  aws_acm_certificate_validation:
    example:
      certificate_arn: ${aws_acm_certificate.example.arn}
      validation_record_fqdns: 'example-list'

resource:
  aws_lb_listener:
    example:
      certificate_arn: ${aws_acm_certificate_validation.example.certificate_arn}
```

## Email Validation

```yaml
resource:
  aws_acm_certificate:
    example:
      domain_name: example.com
      validation_method: EMAIL

resource:
  aws_acm_certificate_validation:
    example:
      certificate_arn: ${aws_acm_certificate.example.arn}
```
