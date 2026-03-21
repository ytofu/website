# FSX Openzfs File System

Manage FSX Openzfs File System resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fsx_openzfs_file_system:
    test:
      storage_capacity: 64
      subnet_ids: 
        - ${aws_subnet.test1.id}
      deployment_type: SINGLE_AZ_1
      throughput_capacity: 64
```
