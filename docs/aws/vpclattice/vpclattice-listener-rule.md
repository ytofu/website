# Vpclattice Listener Rule

Manage Vpclattice Listener Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_listener_rule:
    example:
      name: example
      listener_identifier: ${aws_vpclattice_listener.example.listener_id}
      service_identifier: ${aws_vpclattice_service.example.id}
      priority: 20
      match:
        http_match:
          header_matches:
            name: example-header
            case_sensitive: false
            match:
              exact: example-contains
          path_match:
            case_sensitive: true
            match:
              prefix: /example-path
      action:
        forward:
          target_groups:
            target_group_identifier: ${aws_vpclattice_target_group.example.id}
            weight: 1
          target_groups:
            target_group_identifier: ${aws_vpclattice_target_group.example2.id}
            weight: 2
```

## Basic Usage

```yaml
resource:
  aws_vpclattice_listener_rule:
    example:
      name: example
      listener_identifier: ${aws_vpclattice_listener.example.listener_id}
      service_identifier: ${aws_vpclattice_service.example.id}
      priority: 10
      match:
        http_match:
          path_match:
            case_sensitive: false
            match:
              exact: /example-path
      action:
        fixed_response:
          status_code: 404
```
