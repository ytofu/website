# Resource: aws_route53_hosted_zone_dnssec

Manages Route 53 Hosted Zone Domain Name System Security Extensions (DNSSEC). For more information about managing DNSSEC in Route 53, see the [Route 53 Developer Guide](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec.html).

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_kms_key:
    example:
      customer_master_key_spec: ECC_NIST_P256
      deletion_window_in_days: 7
      key_usage: SIGN_VERIFY
      policy: '{ "Statement": [ { "Action": [ "kms:DescribeKey", "kms:GetPublicKey", "kms:Sign", "kms:Verify", ], "Effect": "Allow" "Principal": { "Service": "dnssec-route53.amazonaws.com" } "Resource": "*" "Sid": "Allow Route 53 DNSSEC Service", }, { "Action": "kms:*" "Effect": "Allow" "Principal": { "AWS": "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root" } "Resource": "*" "Sid": "Enable IAM User Permissions" }, ] "Version": "2012-10-17" }'

  aws_route53_zone:
    example:
      name: example.com

  aws_route53_key_signing_key:
    example:
      hosted_zone_id: ${aws_route53_zone.example.id}
      key_management_service_arn: ${aws_kms_key.example.arn}
      name: example

  aws_route53_hosted_zone_dnssec:
    example:
      depends_on:
        - ${aws_route53_key_signing_key.example}
      hosted_zone_id: ${aws_route53_key_signing_key.example.hosted_zone_id}```

## Argument Reference

The following arguments are required:

* `hosted_zone_id` - (Required) Identifier of the Route 53 Hosted Zone.

The following arguments are optional:

* `signing_status` - (Optional) Hosted Zone signing status. Valid values: `SIGNING`, `NOT_SIGNING`. Defaults to `SIGNING`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Route 53 Hosted Zone identifier.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_route53_hosted_zone_dnssec.example Z1D633PJN98FT9
```
