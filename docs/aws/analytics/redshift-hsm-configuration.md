# Redshift Hsm Configuration

Manage Redshift Hsm Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_hsm_configuration:
    example:
      description: example
      hsm_configuration_identifier: example
      hsm_ip_address: 10.0.0.1
      hsm_partition_name: aws
      hsm_partition_password: example
      hsm_server_public_certificate: example
```
