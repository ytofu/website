# Cloudfront Continuous Deployment Policy

Manage Cloudfront Continuous Deployment Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudfront_distribution:
    staging:
      enabled: true
      staging: true

resource:
  aws_cloudfront_continuous_deployment_policy:
    example:
      enabled: true
      staging_distribution_dns_names:
        items: 
          - ${aws_cloudfront_distribution.staging.domain_name}
        quantity: 1
      traffic_config:
        type: SingleWeight
        single_weight_config:
          weight: 0.01

resource:
  aws_cloudfront_distribution:
    production:
      enabled: true
      continuous_deployment_policy_id: ${aws_cloudfront_continuous_deployment_policy.example.id}
```

## Single Weight Config with Session Stickiness

```yaml
resource:
  aws_cloudfront_continuous_deployment_policy:
    example:
      enabled: true
      staging_distribution_dns_names:
        items: 
          - ${aws_cloudfront_distribution.staging.domain_name}
        quantity: 1
      traffic_config:
        type: SingleWeight
        single_weight_config:
          weight: 0.01
          session_stickiness_config:
            idle_ttl: 300
            maximum_ttl: 600
```

## Single Header Config

```yaml
resource:
  aws_cloudfront_continuous_deployment_policy:
    example:
      enabled: true
      staging_distribution_dns_names:
        items: 
          - ${aws_cloudfront_distribution.staging.domain_name}
        quantity: 1
      traffic_config:
        type: SingleHeader
        single_header_config:
          header: aws-cf-cd-example
          value: example
```
