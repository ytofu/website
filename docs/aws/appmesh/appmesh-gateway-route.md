# Appmesh Gateway Route

Manage Appmesh Gateway Route resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appmesh_gateway_route:
    example:
      name: example-gateway-route
      mesh_name: example-service-mesh
      virtual_gateway_name: ${aws_appmesh_virtual_gateway.example.name}
      spec:
        http_route:
          action:
            target:
              virtual_service:
                virtual_service_name: ${aws_appmesh_virtual_service.example.name}
          match:
            prefix: /
      tags:
        Environment: test
```
