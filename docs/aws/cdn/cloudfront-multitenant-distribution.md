# Cloudfront Multitenant Distribution

Manage Cloudfront Multitenant Distribution resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudfront_multitenant_distribution:
    example:
      comment: Multi-tenant distribution for my application
      enabled: true
      origin:
        domain_name: example.com
        id: example-origin
        custom_origin_config:
          http_port: 80
          https_port: 443
          origin_protocol_policy: https-only
          origin_ssl_protocols: 
            - TLSv1.2
      default_cache_behavior:
        target_origin_id: example-origin
        viewer_protocol_policy: redirect-to-https
        cache_policy_id: ${aws_cloudfront_cache_policy.example.id}
        allowed_methods:
          items: 
            - DELETE
            - GET
            - HEAD
            - OPTIONS
            - PATCH
            - POST
            - PUT
          cached_methods: 
            - GET
            - HEAD
      restrictions:
        geo_restriction:
          restriction_type: none
      viewer_certificate:
        acm_certificate_arn: ${aws_acm_certificate.example.arn}
        ssl_support_method: sni-only
      tenant_config:
        parameter_definition:
          name: origin_domain
          definition:
            string_schema:
              required: true
              comment: Origin domain parameter for tenants
      tags:
        Environment: production
```
