# Vpclattice Listener

Manage Vpclattice Listener resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_service:
    example:
      name: example

resource:
  aws_vpclattice_listener:
    example:
      name: example
      protocol: HTTPS
      service_identifier: ${aws_vpclattice_service.example.id}
      default_action:
        fixed_response:
          status_code: 404
```

## Forward action

```yaml
resource:
  aws_vpclattice_service:
    example:
      name: example

resource:
  aws_vpclattice_target_group:
    example:
      name: example-target-group-1
      type: INSTANCE
      config:
        port: 80
        protocol: HTTP
        vpc_identifier: ${aws_vpc.example.id}

resource:
  aws_vpclattice_listener:
    example:
      name: example
      protocol: HTTP
      service_identifier: ${aws_vpclattice_service.example.id}
      default_action:
        forward:
          target_groups:
            target_group_identifier: ${aws_vpclattice_target_group.example.id}
```

## Forward action with weighted target groups

```yaml
resource:
  aws_vpclattice_service:
    example:
      name: example

resource:
  aws_vpclattice_target_group:
    example1:
      name: example-target-group-1
      type: INSTANCE
      config:
        port: 80
        protocol: HTTP
        vpc_identifier: ${aws_vpc.example.id}

resource:
  aws_vpclattice_target_group:
    example2:
      name: example-target-group-2
      type: INSTANCE
      config:
        port: 8080
        protocol: HTTP
        vpc_identifier: ${aws_vpc.example.id}

resource:
  aws_vpclattice_listener:
    example:
      name: example
      protocol: HTTP
      service_identifier: ${aws_vpclattice_service.example.id}
      default_action:
        forward:
          target_groups:
            target_group_identifier: ${aws_vpclattice_target_group.example1.id}
            weight: 80
          target_groups:
            target_group_identifier: ${aws_vpclattice_target_group.example2.id}
            weight: 20
```
