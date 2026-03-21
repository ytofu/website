# SES Domain Dkim

Manage SES Domain Dkim resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ses_domain_identity:
    example:
      domain: example.com

resource:
  aws_ses_domain_dkim:
    example:
      domain: ${aws_ses_domain_identity.example.domain}

resource:
  aws_route53_record:
    example_amazonses_dkim_record:
      zone_id: ABCDEFGHIJ123
      name: "${aws_ses_domain_dkim.example.dkim_tokens[count.index]}._domainkey"
      type: CNAME
      ttl: 600
      records: 
        - "${aws_ses_domain_dkim.example.dkim_tokens[count.index]}.dkim.amazonses.com"
```
