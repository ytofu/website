# Route53 DNSSEC

Enable DNSSEC signing for hosted zones using ytofu YAML.

## Enable DNSSEC

```yaml
resource:
  aws_kms_key:
    example:
      customer_master_key_spec: ECC_NIST_P256
      deletion_window_in_days: 7
      key_usage: SIGN_VERIFY
      policy: ${data.aws_iam_policy_document.example.json}

  aws_route53_key_signing_key:
    example:
      hosted_zone_id: ${aws_route53_zone.example.id}
      key_management_service_arn: ${aws_kms_key.example.arn}
      name: example

  aws_route53_hosted_zone_dnssec:
    example:
      depends_on:
        - aws_route53_key_signing_key.example
      hosted_zone_id: ${aws_route53_key_signing_key.example.hosted_zone_id}
```
