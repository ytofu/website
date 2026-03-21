# M2 Environment

Manage M2 Environment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_m2_environment:
    test:
      name: test-env
      engine_type: bluage
      instance_type: M2.m5.large
      security_groups: 
        - sg-01234567890abcdef
      subnet_ids: 
        - subnet-01234567890abcdef
        - subnet-01234567890abcdea
```

## High Availability

```yaml
resource:
  aws_m2_environment:
    test:
      name: test-env
      engine_type: bluage
      instance_type: M2.m5.large
      security_groups: 
        - sg-01234567890abcdef
      subnet_ids: 
        - subnet-01234567890abcdef
        - subnet-01234567890abcdea
      high_availability_config:
        desired_capacity: 2
```

## EFS Filesystem

```yaml
resource:
  aws_m2_environment:
    test:
      name: test-env
      engine_type: bluage
      instance_type: M2.m5.large
      security_groups: 
        - sg-01234567890abcdef
      subnet_ids: 
        - subnet-01234567890abcdef
        - subnet-01234567890abcdea
      storage_configuration:
        efs:
          file_system_id: fs-01234567890abcdef
          mount_point: /m2/mount/example
```

## FSX Filesystem

```yaml
resource:
  aws_m2_environment:
    test:
      name: test-env
      engine_type: bluage
      instance_type: M2.m5.large
      security_groups: 
        - sg-01234567890abcdef
      subnet_ids: 
        - subnet-01234567890abcdef
        - subnet-01234567890abcdea
      storage_configuration:
        fsx:
          file_system_id: fs-01234567890abcdef
          mount_point: /m2/mount/example
```
