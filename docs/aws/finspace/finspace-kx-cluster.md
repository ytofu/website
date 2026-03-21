# Finspace Kx Cluster

Manage Finspace Kx Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_finspace_kx_cluster:
    example:
      name: my-tf-kx-cluster
      environment_id: ${aws_finspace_kx_environment.example.id}
      type: HDB
      release_label: 1.0
      az_mode: SINGLE
      availability_zone_id: use1-az2
      capacity_configuration:
        node_type: kx.s.2xlarge
        node_count: 2
      vpc_configuration:
        vpc_id: ${aws_vpc.test.id}
        security_group_ids: 
          - ${aws_security_group.example.id}
        subnet_ids: 
          - ${aws_subnet.example.id}
        ip_address_type: IP_V4
      cache_storage_configurations:
        type: CACHE_1000
        size: 1200
      database:
        database_name: ${aws_finspace_kx_database.example.name}
        cache_configuration:
          cache_type: CACHE_1000
          db_paths: /
      code:
        s3_bucket: ${aws_s3_bucket.test.id}
        s3_key: ${aws_s3_object.object.key}
      timeouts:
        create: 18h
        update: 18h
```
