# FSX Ontap Storage Virtual Machine

Manage FSX Ontap Storage Virtual Machine resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fsx_ontap_storage_virtual_machine:
    test:
      file_system_id: ${aws_fsx_ontap_file_system.test.id}
      name: test
```

## Using a Self-Managed Microsoft Active Directory

```yaml
resource:
  aws_fsx_ontap_storage_virtual_machine:
    test:
      file_system_id: ${aws_fsx_ontap_file_system.test.id}
      name: mysvm
      active_directory_configuration:
        netbios_name: mysvm
        self_managed_active_directory_configuration:
          dns_ips: 
            - 10.0.0.111
            - 10.0.0.222
          domain_name: corp.example.com
          password: avoid-plaintext-passwords
          username: Admin
```
