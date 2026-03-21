# Verifiedaccess Endpoint

Manage Verifiedaccess Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_verifiedaccess_endpoint:
    example:
      application_domain: example.com
      attachment_type: vpc
      description: example
      domain_certificate_arn: ${aws_acm_certificate.example.arn}
      endpoint_domain_prefix: example
      endpoint_type: load-balancer
      load_balancer_options:
        load_balancer_arn: ${aws_lb.example.arn}
        port: 443
        protocol: https
        subnet_ids: 
          - example-map
      security_group_ids: 
        - ${aws_security_group.example.id}
      verified_access_group_id: ${aws_verifiedaccess_group.example.id}
```

## Network Interface Example

```yaml
resource:
  aws_verifiedaccess_endpoint:
    example:
      application_domain: example.com
      attachment_type: vpc
      description: example
      domain_certificate_arn: ${aws_acm_certificate.example.arn}
      endpoint_domain_prefix: example
      endpoint_type: network-interface
      network_interface_options:
        network_interface_id: ${aws_network_interface.example.id}
        port: 443
        protocol: https
      security_group_ids: 
        - ${aws_security_group.example.id}
      verified_access_group_id: ${aws_verifiedaccess_group.example.id}
```

## Cidr Example

```yaml
resource:
  aws_verifiedaccess_endpoint:
    example:
      attachment_type: vpc
      description: example
      endpoint_type: cidr
      cidr_options:
        cidr: ${aws_subnet.test[0].cidr_block}
        port_range:
          from_port: 443
          to_port: 443
        protocol: tcp
        subnet_ids: 
          - example-map
      security_group_ids: 
        - ${aws_security_group.test.id}
      verified_access_group_id: ${aws_verifiedaccess_group.test.id}
```
