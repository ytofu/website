# Cloudfront VPC Origin

Manage Cloudfront VPC Origin resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudfront_vpc_origin:
    alb:
      vpc_origin_endpoint_config:
        name: example-vpc-origin
        arn: ${aws_lb.this.arn}
        http_port: 8080
        https_port: 8443
        origin_protocol_policy: https-only
        origin_ssl_protocols:
          items: 
            - TLSv1.2
          quantity: 1
```
