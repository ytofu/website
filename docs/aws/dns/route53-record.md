# Route53 Record

Manage Route53 Record resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_record:
    www:
      zone_id: ${aws_route53_zone.primary.zone_id}
      name: www.example.com
      type: A
      ttl: 300
      records: 
        - ${aws_eip.lb.public_ip}
```

## Weighted routing policy

```yaml
resource:
  aws_route53_record:
    www-dev:
      zone_id: ${aws_route53_zone.primary.zone_id}
      name: www
      type: CNAME
      ttl: 5
      weighted_routing_policy:
        weight: 10
      set_identifier: dev
      records: 
        - dev.example.com

resource:
  aws_route53_record:
    www-live:
      zone_id: ${aws_route53_zone.primary.zone_id}
      name: www
      type: CNAME
      ttl: 5
      weighted_routing_policy:
        weight: 90
      set_identifier: live
      records: 
        - live.example.com
```

## Geoproximity routing policy

```yaml
resource:
  aws_route53_record:
    www:
      zone_id: ${aws_route53_zone.primary.zone_id}
      name: www.example.com
      type: CNAME
      ttl: 300
      geoproximity_routing_policy:
        coordinates:
          latitude: 49.22
          longitude: -74.01
      set_identifier: dev
      records: 
        - dev.example.com
```

## Alias record

```yaml
resource:
  aws_elb:
    main:
      name: foobar-terraform-elb
      availability_zones: 
        - us-east-1c
      listener:
        instance_port: 80
        instance_protocol: http
        lb_port: 80
        lb_protocol: http

resource:
  aws_route53_record:
    www:
      zone_id: ${aws_route53_zone.primary.zone_id}
      name: example.com
      type: A
      alias:
        name: ${aws_elb.main.dns_name}
        zone_id: ${aws_elb.main.zone_id}
        evaluate_target_health: true
```

## Alias record for AWS Global Accelerator

```yaml
resource:
  aws_globalaccelerator_accelerator:
    main:
      name: foobar-terraform-accelerator
      enabled: true
      ip_address_type: IPV4

resource:
  aws_route53_record:
    www:
      zone_id: ${aws_route53_zone.primary.zone_id}
      name: example.com
      type: A
      alias:
        name: ${aws_globalaccelerator_accelerator.main.dns_name}
        zone_id: ${aws_globalaccelerator_accelerator.main.hosted_zone_id}
        evaluate_target_health: false
```

## NS and SOA Record Management

```yaml
resource:
  aws_route53_zone:
    example:
      name: test.example.com

resource:
  aws_route53_record:
    example:
      allow_overwrite: true
      name: test.example.com
      ttl: 172800
      type: NS
      zone_id: ${aws_route53_zone.example.zone_id}
      records:
        - ${aws_route53_zone.example.name_servers[0]}
        - ${aws_route53_zone.example.name_servers[1]}
        - ${aws_route53_zone.example.name_servers[2]}
        - ${aws_route53_zone.example.name_servers[3]}
```
