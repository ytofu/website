# Directory Service Conditional Forwarder

Manage Directory Service Conditional Forwarder resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_directory_service_conditional_forwarder:
    example:
      directory_id: ${aws_directory_service_directory.ad.id}
      remote_domain_name: example.com
      dns_ips:
        - 8.8.8.8
        - 8.8.4.4
```
