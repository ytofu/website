# SES Configuration Set

Manage SES Configuration Set resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ses_configuration_set:
    test:
      name: some-configuration-set-test
```

## Require TLS Connections

```yaml
resource:
  aws_ses_configuration_set:
    test:
      name: some-configuration-set-test
      delivery_options:
        tls_policy: Require
```

## Tracking Options

```yaml
resource:
  aws_ses_configuration_set:
    test:
      name: some-configuration-set-test
      tracking_options:
        custom_redirect_domain: sub.example.com
```
