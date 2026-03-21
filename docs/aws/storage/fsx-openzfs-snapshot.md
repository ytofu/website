# FSX Openzfs Snapshot

Manage FSX Openzfs Snapshot resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fsx_openzfs_snapshot:
    example:
      name: example
      volume_id: ${aws_fsx_openzfs_file_system.example.root_volume_id}

resource:
  aws_fsx_openzfs_file_system:
    example:
      storage_capacity: 64
      subnet_ids: 
        - ${aws_subnet.example.id}
      deployment_type: SINGLE_AZ_1
      throughput_capacity: 64
```

## Child volume Example

```yaml
resource:
  aws_fsx_openzfs_snapshot:
    example:
      name: example
      volume_id: ${aws_fsx_openzfs_volume.example.id}

resource:
  aws_fsx_openzfs_volume:
    example:
      name: example
      parent_volume_id: ${aws_fsx_openzfs_file_system.example.root_volume_id}

resource:
  aws_fsx_openzfs_file_system:
    example:
      storage_capacity: 64
      subnet_ids: 
        - ${aws_subnet.example.id}
      deployment_type: SINGLE_AZ_1
      throughput_capacity: 64
```
