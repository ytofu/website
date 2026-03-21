# Vpclattice Resource Configuration

Manage Vpclattice Resource Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_resource_configuration:
    example:
      name: Example
      resource_gateway_identifier: ${aws_vpclattice_resource_gateway.example.id}
      port_ranges: 
        - 80
      protocol: TCP
      resource_configuration_definition:
        dns_resource:
          domain_name: example.com
          ip_address_type: IPV4
      tags:
        Environment: Example
```

## IP Address Example

```yaml
resource:
  aws_vpclattice_resource_configuration:
    example:
      name: Example
      resource_gateway_identifier: ${aws_vpclattice_resource_gateway.example.id}
      port_ranges: 
        - 80
      protocol: TCP
      resource_configuration_definition:
        ip_resource:
          ip_address: 10.0.0.1
      tags:
        Environment: Example
```

## With custom domain

```yaml
resource:
  aws_vpclattice_domain_verification:
    example:
      domain_name: example.com

resource:
  aws_vpclattice_resource_configuration:
    example:
      name: Example
      resource_gateway_identifier: ${aws_vpclattice_resource_gateway.example.id}
      custom_domain_name: custom.example.com
      domain_verification_id: ${aws_vpclattice_domain_verification.example.id}
      port_ranges: 
        - 443
      protocol: TCP
      resource_configuration_definition:
        dns_resource:
          domain_name: test.example.com
          ip_address_type: IPV4
      tags:
        Environment: Example
```

## ARN Example

```yaml
resource:
  aws_vpclattice_resource_configuration:
    test:
      name: Example
      resource_gateway_identifier: ${aws_vpclattice_resource_gateway.test.id}
      type: ARN
      resource_configuration_definition:
        arn_resource:
          arn: ${aws_rds_cluster_instance.example.arn}
```
