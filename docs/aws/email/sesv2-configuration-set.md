# Sesv2 Configuration Set

Manage Sesv2 Configuration Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sesv2_configuration_set:
    example:
      configuration_set_name: example
      delivery_options:
        max_delivery_seconds: 300
        tls_policy: REQUIRE
      reputation_options:
        reputation_metrics_enabled: false
      sending_options:
        sending_enabled: true
      suppression_options:
        suppressed_reasons: 
          - BOUNCE
          - COMPLAINT
      tracking_options:
        custom_redirect_domain: example.com
        https_policy: REQUIRE
```
