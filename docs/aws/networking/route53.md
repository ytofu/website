# Route53

Manage DNS with Amazon Route53 using ytofu YAML.

## Hosted Zone

### Public Hosted Zone

```yaml
resource:
  aws_route53_zone:
    main:
      name: example.com
      tags:
        Name: example.com
```

### Private Hosted Zone

```yaml
resource:
  aws_route53_zone:
    private:
      name: internal.example.com

      vpc:
        - vpc_id: ${aws_vpc.main.id}

      tags:
        Name: internal.example.com
```

## Arguments Reference (Hosted Zone)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| name | string | Yes | Domain name |
| vpc | list | No | VPCs for private zone |
| comment | string | No | Zone comment |
| force_destroy | bool | No | Delete records on zone deletion |
| tags | map | No | Resource tags |

## DNS Records

### A Record

```yaml
resource:
  aws_route53_record:
    www:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: www.example.com
      type: A
      ttl: 300
      records:
        - 192.0.2.1
```

### A Record with Alias (for ALB)

```yaml
resource:
  aws_route53_record:
    app:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: app.example.com
      type: A

      alias:
        name: ${aws_lb.main.dns_name}
        zone_id: ${aws_lb.main.zone_id}
        evaluate_target_health: true
```

### CNAME Record

```yaml
resource:
  aws_route53_record:
    mail:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: mail.example.com
      type: CNAME
      ttl: 300
      records:
        - mail.provider.com
```

### MX Records

```yaml
resource:
  aws_route53_record:
    mx:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: example.com
      type: MX
      ttl: 300
      records:
        - "10 mail1.example.com"
        - "20 mail2.example.com"
```

### TXT Record

```yaml
resource:
  aws_route53_record:
    txt:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: example.com
      type: TXT
      ttl: 300
      records:
        - "v=spf1 include:_spf.google.com ~all"
```

## Arguments Reference (Record)

| Argument | Type | Required | Description |
|----------|------|----------|-------------|
| zone_id | string | Yes | Hosted zone ID |
| name | string | Yes | Record name |
| type | string | Yes | A, AAAA, CNAME, MX, TXT, etc. |
| ttl | number | No* | Time to live in seconds |
| records | list | No* | Record values |
| alias | object | No* | Alias target configuration |

*Either ttl+records or alias required

## Common Patterns

### Complete Website Setup

```yaml
resource:
  aws_route53_zone:
    main:
      name: example.com

  # Root domain -> ALB
  aws_route53_record:
    root:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: example.com
      type: A
      alias:
        name: ${aws_lb.main.dns_name}
        zone_id: ${aws_lb.main.zone_id}
        evaluate_target_health: true

  # www -> Root
  aws_route53_record:
    www:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: www.example.com
      type: A
      alias:
        name: example.com
        zone_id: ${aws_route53_zone.main.zone_id}
        evaluate_target_health: false
```

### ACM Certificate Validation

```yaml
resource:
  aws_acm_certificate:
    main:
      domain_name: example.com
      subject_alternative_names:
        - "*.example.com"
      validation_method: DNS

  # Create validation record for each domain
  aws_route53_record:
    cert_validation_main:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: _acme-challenge.example.com
      type: CNAME
      ttl: 60
      records:
        - _validation-token.acm-validations.aws.
      allow_overwrite: true

    cert_validation_wildcard:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: _acme-challenge.example.com
      type: CNAME
      ttl: 60
      records:
        - _validation-token.acm-validations.aws.
      allow_overwrite: true

  aws_acm_certificate_validation:
    main:
      certificate_arn: ${aws_acm_certificate.main.arn}
      validation_record_fqdns:
        - ${aws_route53_record.cert_validation_main.fqdn}
        - ${aws_route53_record.cert_validation_wildcard.fqdn}
```

> **Note:** The actual validation record names and values are provided by ACM after certificate creation. In practice, you would retrieve these values and create the records accordingly.


### Weighted Routing

```yaml
resource:
  aws_route53_record:
    blue:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: api.example.com
      type: A
      set_identifier: blue

      alias:
        name: ${aws_lb.blue.dns_name}
        zone_id: ${aws_lb.blue.zone_id}
        evaluate_target_health: true

      weighted_routing_policy:
        weight: 90

    green:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: api.example.com
      type: A
      set_identifier: green

      alias:
        name: ${aws_lb.green.dns_name}
        zone_id: ${aws_lb.green.zone_id}
        evaluate_target_health: true

      weighted_routing_policy:
        weight: 10
```

### Geolocation Routing

```yaml
resource:
  aws_route53_record:
    us:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: api.example.com
      type: A
      set_identifier: us

      alias:
        name: ${aws_lb.us.dns_name}
        zone_id: ${aws_lb.us.zone_id}
        evaluate_target_health: true

      geolocation_routing_policy:
        country: US

    eu:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: api.example.com
      type: A
      set_identifier: eu

      alias:
        name: ${aws_lb.eu.dns_name}
        zone_id: ${aws_lb.eu.zone_id}
        evaluate_target_health: true

      geolocation_routing_policy:
        continent: EU

    default:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: api.example.com
      type: A
      set_identifier: default

      alias:
        name: ${aws_lb.us.dns_name}
        zone_id: ${aws_lb.us.zone_id}
        evaluate_target_health: true

      geolocation_routing_policy:
        country: "*"
```

### Failover Routing

```yaml
resource:
  aws_route53_health_check:
    primary:
      fqdn: primary.example.com
      port: 443
      type: HTTPS
      resource_path: /health
      failure_threshold: 3
      request_interval: 30

  aws_route53_record:
    primary:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: api.example.com
      type: A
      set_identifier: primary
      health_check_id: ${aws_route53_health_check.primary.id}

      alias:
        name: ${aws_lb.primary.dns_name}
        zone_id: ${aws_lb.primary.zone_id}
        evaluate_target_health: true

      failover_routing_policy:
        type: PRIMARY

    secondary:
      zone_id: ${aws_route53_zone.main.zone_id}
      name: api.example.com
      type: A
      set_identifier: secondary

      alias:
        name: ${aws_lb.secondary.dns_name}
        zone_id: ${aws_lb.secondary.zone_id}
        evaluate_target_health: true

      failover_routing_policy:
        type: SECONDARY
```

## Attributes Reference

### Hosted Zone

| Attribute | Description |
|-----------|-------------|
| zone_id | Hosted zone ID |
| name_servers | Name server list |
| arn | Hosted zone ARN |

### Record

| Attribute | Description |
|-----------|-------------|
| name | Record name |
| fqdn | Fully qualified domain name |

## Best Practices

- **Use aliases** for AWS resources instead of CNAMEs
- **Enable health checks** for failover scenarios
- **Set appropriate TTLs** (lower for dynamic, higher for static)
- **Use private zones** for internal services
- **Implement DNSSEC** for security
- **Monitor with CloudWatch**

## Common Record Types

| Type | Use Case |
|------|----------|
| A | IPv4 address |
| AAAA | IPv6 address |
| CNAME | Alias to another domain |
| MX | Mail servers |
| TXT | Text records (SPF, DKIM) |
| NS | Name servers |
| SOA | Zone authority |
| SRV | Service location |
| CAA | Certificate authority |

## Related Resources

- [Load Balancer](load-balancer.md)
- [ACM Certificate](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/acm_certificate)
- [CloudFront](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudfront_distribution)
