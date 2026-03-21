# Lightsail Distribution

Manage Lightsail Distribution resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lightsail_bucket:
    example:
      name: example-bucket
      bundle_id: small_1_0

resource:
  aws_lightsail_distribution:
    example:
      name: example-distribution
      bundle_id: small_1_0
      origin:
        name: ${aws_lightsail_bucket.example.name}
        region_name: ${aws_lightsail_bucket.example.region}
      default_cache_behavior:
        behavior: cache
      cache_behavior_settings:
        allowed_http_methods: GET,HEAD,OPTIONS,PUT,PATCH,POST,DELETE
        cached_http_methods: GET,HEAD
        default_ttl: 86400
        maximum_ttl: 31536000
        minimum_ttl: 0
        forwarded_cookies:
          option: none
        forwarded_headers:
          option: default
        forwarded_query_strings:
          option: false
```

## Instance Origin

```yaml
data:
  aws_availability_zones:
    available:
      state: available
      filter:
        name: opt-in-status
        values: 
          - opt-in-not-required

resource:
  aws_lightsail_static_ip_attachment:
    example:
      static_ip_name: ${aws_lightsail_static_ip.example.name}
      instance_name: ${aws_lightsail_instance.example.name}

resource:
  aws_lightsail_static_ip:
    example:
      name: example-static-ip

resource:
  aws_lightsail_instance:
    example:
      name: example-instance
      availability_zone: ${data.aws_availability_zones.available.names[0]}
      blueprint_id: amazon_linux_2
      bundle_id: micro_1_0

resource:
  aws_lightsail_distribution:
    example:
      name: example-distribution
      depends_on: 
        - ${aws_lightsail_static_ip_attachment.example}
      bundle_id: small_1_0
      origin:
        name: ${aws_lightsail_instance.example.name}
        region_name: ${data.aws_availability_zones.available.id}
      default_cache_behavior:
        behavior: cache
```

## Load Balancer Origin

```yaml
data:
  aws_availability_zones:
    available:
      state: available
      filter:
        name: opt-in-status
        values: 
          - opt-in-not-required

resource:
  aws_lightsail_lb:
    example:
      name: example-load-balancer
      health_check_path: /
      instance_port: 80
      tags:
        foo: bar

resource:
  aws_lightsail_instance:
    example:
      name: example-instance
      availability_zone: ${data.aws_availability_zones.available.names[0]}
      blueprint_id: amazon_linux_2
      bundle_id: nano_3_0

resource:
  aws_lightsail_lb_attachment:
    example:
      lb_name: ${aws_lightsail_lb.example.name}
      instance_name: ${aws_lightsail_instance.example.name}

resource:
  aws_lightsail_distribution:
    example:
      name: example-distribution
      depends_on: 
        - ${aws_lightsail_lb_attachment.example}
      bundle_id: small_1_0
      origin:
        name: ${aws_lightsail_lb.example.name}
        region_name: ${data.aws_availability_zones.available.id}
      default_cache_behavior:
        behavior: cache
```
