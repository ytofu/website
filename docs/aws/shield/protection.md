# Shield Protection

Enable Shield Advanced protection for resources using ytofu YAML.

## Protect EIP

```yaml
resource:
  aws_shield_protection:
    example:
      name: eip-protection
      resource_arn: ${aws_eip.example.arn}
```

## Protect ALB

```yaml
resource:
  aws_shield_protection:
    alb:
      name: alb-protection
      resource_arn: ${aws_lb.example.arn}
      tags:
        Environment: production
```

## Protect CloudFront

```yaml
resource:
  aws_shield_protection:
    cdn:
      name: cloudfront-protection
      resource_arn: ${aws_cloudfront_distribution.example.arn}
```
