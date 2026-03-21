# Appmesh Route

Manage Appmesh Route resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appmesh_route:
    serviceb:
      name: serviceB-route
      mesh_name: ${aws_appmesh_mesh.simple.id}
      virtual_router_name: ${aws_appmesh_virtual_router.serviceb.name}
      spec:
        http_route:
          match:
            prefix: /
          action:
            weighted_target:
              virtual_node: ${aws_appmesh_virtual_node.serviceb1.name}
              weight: 90
            weighted_target:
              virtual_node: ${aws_appmesh_virtual_node.serviceb2.name}
              weight: 10
```

## HTTP Header Routing

```yaml
resource:
  aws_appmesh_route:
    serviceb:
      name: serviceB-route
      mesh_name: ${aws_appmesh_mesh.simple.id}
      virtual_router_name: ${aws_appmesh_virtual_router.serviceb.name}
      spec:
        http_route:
          match:
            method: POST
            prefix: /
            scheme: https
            header:
              name: clientRequestId
              match:
                prefix: 123
          action:
            weighted_target:
              virtual_node: ${aws_appmesh_virtual_node.serviceb.name}
              weight: 100
```

## Retry Policy

```yaml
resource:
  aws_appmesh_route:
    serviceb:
      name: serviceB-route
      mesh_name: ${aws_appmesh_mesh.simple.id}
      virtual_router_name: ${aws_appmesh_virtual_router.serviceb.name}
      spec:
        http_route:
          match:
            prefix: /
          retry_policy:
            http_retry_events:
              - server-error
            max_retries: 1
            per_retry_timeout:
              unit: s
              value: 15
          action:
            weighted_target:
              virtual_node: ${aws_appmesh_virtual_node.serviceb.name}
              weight: 100
```

## TCP Routing

```yaml
resource:
  aws_appmesh_route:
    serviceb:
      name: serviceB-route
      mesh_name: ${aws_appmesh_mesh.simple.id}
      virtual_router_name: ${aws_appmesh_virtual_router.serviceb.name}
      spec:
        tcp_route:
          action:
            weighted_target:
              virtual_node: ${aws_appmesh_virtual_node.serviceb1.name}
              weight: 100
```
