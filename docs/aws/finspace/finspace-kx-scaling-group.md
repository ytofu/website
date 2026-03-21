# Finspace Kx Scaling Group

Manage Finspace Kx Scaling Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_finspace_kx_scaling_group:
    example:
      name: my-tf-kx-scalinggroup
      environment_id: ${aws_finspace_kx_environment.example.id}
      availability_zone_id: use1-az2
      host_type: kx.sg.4xlarge
```
