# FSX Openzfs Volume

Manage FSX Openzfs Volume resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fsx_openzfs_volume:
    test:
      name: testvolume
      parent_volume_id: ${aws_fsx_openzfs_file_system.test.root_volume_id}
```
