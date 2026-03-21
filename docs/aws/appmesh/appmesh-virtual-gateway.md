# Appmesh Virtual Gateway

Manage Appmesh Virtual Gateway resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appmesh_virtual_gateway:
    example:
      name: example-virtual-gateway
      mesh_name: example-service-mesh
      spec:
        listener:
          port_mapping:
            port: 8080
            protocol: http
      tags:
        Environment: test
```

## Access Logs and TLS

```yaml
resource:
  aws_appmesh_virtual_gateway:
    example:
      name: example-virtual-gateway
      mesh_name: example-service-mesh
      spec:
        listener:
          port_mapping:
            port: 8080
            protocol: http
          tls:
            certificate:
              acm:
                certificate_arn: ${aws_acm_certificate.example.arn}
            mode: STRICT
        logging:
          access_log:
            file:
              path: /var/log/access.log
```
