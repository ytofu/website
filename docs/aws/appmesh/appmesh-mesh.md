# Appmesh Mesh

Manage Appmesh Mesh resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appmesh_mesh:
    simple:
      name: simpleapp
```

## Egress Filter

```yaml
resource:
  aws_appmesh_mesh:
    simple:
      name: simpleapp
      spec:
        egress_filter:
          type: ALLOW_ALL
```
