# Appmesh Virtual Service

Manage Appmesh Virtual Service resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appmesh_virtual_service:
    servicea:
      name: servicea.simpleapp.local
      mesh_name: ${aws_appmesh_mesh.simple.id}
      spec:
```

## Virtual Router Provider

```yaml
resource:
  aws_appmesh_virtual_service:
    servicea:
      name: servicea.simpleapp.local
      mesh_name: ${aws_appmesh_mesh.simple.id}
      spec:
```
