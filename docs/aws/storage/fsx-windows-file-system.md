# FSX Windows File System

Manage FSX Windows File System resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fsx_windows_file_system:
    example:
      active_directory_id: ${aws_directory_service_directory.example.id}
      kms_key_id: ${aws_kms_key.example.arn}
      storage_capacity: 32
      subnet_ids: 
        - ${aws_subnet.example.id}
      throughput_capacity: 32
```

## Using a Self-Managed Microsoft Active Directory

```yaml
resource:
  aws_fsx_windows_file_system:
    example:
      kms_key_id: ${aws_kms_key.example.arn}
      storage_capacity: 32
      subnet_ids: 
        - ${aws_subnet.example.id}
      throughput_capacity: 32
      self_managed_active_directory:
        dns_ips: 
          - 10.0.0.111
          - 10.0.0.222
        domain_name: corp.example.com
        password: avoid-plaintext-passwords
        username: Admin
```

## Using a Self-Managed Microsoft Active Directory with Secrets Manager

```yaml
resource:
  aws_fsx_windows_file_system:
    example:
      kms_key_id: ${aws_kms_key.example.arn}
      storage_capacity: 32
      subnet_ids: 
        - ${aws_subnet.example.id}
      throughput_capacity: 32
      self_managed_active_directory:
        dns_ips: 
          - 10.0.0.111
          - 10.0.0.222
        domain_name: corp.example.com
        domain_join_service_account_secret: ${aws_secretsmanager_secret.example.arn}
```
