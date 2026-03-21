# Finspace Kx Volume

Manage Finspace Kx Volume resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_finspace_kx_volume:
    example:
      name: my-tf-kx-volume
      environment_id: ${aws_finspace_kx_environment.example.id}
      availability_zones: 
        - use1-az2
      az_mode: SINGLE
      type: NAS_1
      nas1_configuration:
        size: 1200
        type: SSD_250
```
