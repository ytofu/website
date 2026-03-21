# FSX Ontap Volume

Manage FSX Ontap Volume resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fsx_ontap_volume:
    test:
      name: test
      junction_path: /test
      size_in_megabytes: 1024
      storage_efficiency_enabled: true
      storage_virtual_machine_id: ${aws_fsx_ontap_storage_virtual_machine.test.id}
```

## Using Tiering Policy

```yaml
resource:
  aws_fsx_ontap_volume:
    test:
      name: test
      junction_path: /test
      size_in_megabytes: 1024
      storage_efficiency_enabled: true
      storage_virtual_machine_id: ${aws_fsx_ontap_storage_virtual_machine.test.id}
      tiering_policy:
        name: AUTO
        cooling_period: 31
```
