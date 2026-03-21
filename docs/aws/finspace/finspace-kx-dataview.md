# Finspace Kx Dataview

Manage Finspace Kx Dataview resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_finspace_kx_dataview:
    example:
      name: my-tf-kx-dataview
      environment_id: ${aws_finspace_kx_environment.example.id}
      database_name: ${aws_finspace_kx_database.example.name}
      availability_zone_id: use1-az2
      description: Terraform managed Kx Dataview
      az_mode: SINGLE
      auto_update: true
      segment_configurations:
        volume_name: ${aws_finspace_kx_volume.example.name}
        db_paths: 
          - "/*"
      timeouts:
        create: 24h
        update: 24h
        delete: 12h
```
