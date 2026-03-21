# VPC Endpoint

Manage VPC Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint:
    s3:
      vpc_id: ${aws_vpc.main.id}
      service_name: com.amazonaws.us-west-2.s3
```

## Basic w/ Tags

```yaml
resource:
  aws_vpc_endpoint:
    s3:
      vpc_id: ${aws_vpc.main.id}
      service_name: com.amazonaws.us-west-2.s3
      tags:
        Environment: test
```

## Cross-region enabled AWS services

```yaml
resource:
  aws_vpc_endpoint:
    s3:
      region: us-west-2
      vpc_id: ${aws_vpc.main.id}
      service_name: com.amazonaws.us-east-2.s3
      service_region: us-east-2
      tags:
        Environment: test
```

## Interface Endpoint Type

```yaml
resource:
  aws_vpc_endpoint:
    ec2:
      vpc_id: ${aws_vpc.main.id}
      service_name: com.amazonaws.us-west-2.ec2
      vpc_endpoint_type: Interface
      security_group_ids:
        - ${aws_security_group.sg1.id}
      private_dns_enabled: true
```

## Interface Endpoint Type with User-Defined IP Address

```yaml
resource:
  aws_vpc_endpoint:
    ec2:
      vpc_id: ${aws_vpc.example.id}
      service_name: com.amazonaws.us-west-2.ec2
      vpc_endpoint_type: Interface
      subnet_configuration:
        ipv4: 10.0.1.10
        subnet_id: ${aws_subnet.example1.id}
      subnet_configuration:
        ipv4: 10.0.2.10
        subnet_id: ${aws_subnet.example2.id}
      subnet_ids:
        - ${aws_subnet.example1.id}
        - ${aws_subnet.example2.id}
```

## Gateway Load Balancer Endpoint Type

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_vpc_endpoint_service:
    example:
      acceptance_required: false
      allowed_principals: 
        - ${data.aws_caller_identity.current.arn}
      gateway_load_balancer_arns: 
        - ${aws_lb.example.arn}

resource:
  aws_vpc_endpoint:
    example:
      service_name: ${aws_vpc_endpoint_service.example.service_name}
      subnet_ids: 
        - ${aws_subnet.example.id}
      vpc_endpoint_type: ${aws_vpc_endpoint_service.example.service_type}
      vpc_id: ${aws_vpc.example.id}
```

## VPC Lattice Resource Configuration Endpoint Type

```yaml
resource:
  aws_vpc_endpoint:
    example:
      resource_configuration_arn: ${aws_vpclattice_resource_configuration.example.arn}
      subnet_ids: 
        - ${aws_subnet.example.id}
      vpc_endpoint_type: Resource
      vpc_id: ${aws_vpc.example.id}
```

## VPC Lattice Service Network Endpoint Type

```yaml
resource:
  aws_vpc_endpoint:
    example:
      service_network_arn: ${aws_vpclattice_service_network.example.arn}
      subnet_ids: 
        - ${aws_subnet.example.id}
      vpc_endpoint_type: ServiceNetwork
      vpc_id: ${aws_vpc.example.id}
```

## Non-AWS Service

```yaml
resource:
  aws_vpc_endpoint:
    ptfe_service:
      vpc_id: example-vpc_id
      service_name: example-ptfe_service
      vpc_endpoint_type: Interface
      security_group_ids:
        - ${aws_security_group.ptfe_service.id}
      subnet_ids: 
        - example-subnet_ids
      private_dns_enabled: false

data:
  aws_route53_zone:
    internal:
      name: vpc.internal.
      private_zone: true
      vpc_id: example-vpc_id

resource:
  aws_route53_record:
    ptfe_service:
      zone_id: ${data.aws_route53_zone.internal.zone_id}
      name: "ptfe.${data.aws_route53_zone.internal.name}"
      type: CNAME
      ttl: 300
      records: 
        - ${aws_vpc_endpoint.ptfe_service.dns_entry[0]["dns_name"]}
```
