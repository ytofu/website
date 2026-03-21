# VPC Lattice Target Group

Create target groups for VPC Lattice using ytofu YAML.

## Instance Target Group

```yaml
resource:
  aws_vpclattice_target_group:
    example:
      name: example
      type: INSTANCE
      config:
        port: 80
        protocol: HTTP
        vpc_identifier: ${aws_vpc.example.id}
```

## Lambda Target Group

```yaml
resource:
  aws_vpclattice_target_group:
    lambda:
      name: lambda-target
      type: LAMBDA
```

## ALB Target Group

```yaml
resource:
  aws_vpclattice_target_group:
    alb:
      name: alb-target
      type: ALB
      config:
        port: 80
        protocol: HTTP
        vpc_identifier: ${aws_vpc.example.id}
```
