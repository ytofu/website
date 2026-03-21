# VPC Lattice Service

Create VPC Lattice services using ytofu YAML.

## Basic Service

```yaml
resource:
  aws_vpclattice_service:
    example:
      name: example
      auth_type: NONE
```

## With IAM Auth

```yaml
resource:
  aws_vpclattice_service:
    example:
      name: example
      auth_type: AWS_IAM
      custom_domain_name: api.example.com
      certificate_arn: ${aws_acm_certificate.example.arn}
```

## Service Network Association

```yaml
resource:
  aws_vpclattice_service_network_service_association:
    example:
      service_identifier: ${aws_vpclattice_service.example.id}
      service_network_identifier: ${aws_vpclattice_service_network.example.id}
```
