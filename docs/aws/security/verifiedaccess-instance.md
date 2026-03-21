# Verifiedaccess Instance

Manage Verifiedaccess Instance resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_verifiedaccess_instance:
    example:
      description: example
      tags:
        Name: example
```

## With `fips_enabled`

```yaml
resource:
  aws_verifiedaccess_instance:
    example:
      fips_enabled: true
```

## With `cidr_endpoints_custom_subdomain`

```yaml
resource:
  aws_verifiedaccess_instance:
    example:
      cidr_endpoints_custom_subdomain: test.example.com
```
