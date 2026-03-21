# Cloudfront Distribution Tenant

Manage Cloudfront Distribution Tenant resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudfront_distribution_tenant:
    example:
      name: example-tenant
      distribution_id: ${aws_cloudfront_multitenant_distribution.example.id}
      enabled: true
      domain:
        domain: tenant.example.com
      tags:
        Environment: production
```

## Distribution Tenant with Customizations

```yaml
resource:
  aws_cloudfront_distribution_tenant:
    example:
      name: example-tenant
      distribution_id: ${aws_cloudfront_multitenant_distribution.example.id}
      enabled: false
      domain:
        domain: tenant.example.com
      customizations:
        geo_restriction:
          restriction_type: whitelist
          locations: 
            - US
            - CA
        certificate:
          arn: ${aws_acm_certificate.tenant_cert.arn}
        web_acl:
          action: override
          arn: ${aws_wafv2_web_acl.tenant_waf.arn}
      tags:
        Environment: production
        Tenant: example
```
