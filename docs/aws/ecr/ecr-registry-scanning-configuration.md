# ECR Registry Scanning Configuration

Manage ECR Registry Scanning Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecr_registry_scanning_configuration:
    configuration:
      scan_type: ENHANCED
      rule:
        scan_frequency: CONTINUOUS_SCAN
        repository_filter:
          filter: example
          filter_type: WILDCARD
```

## Multiple rules

```yaml
resource:
  aws_ecr_registry_scanning_configuration:
    test:
      scan_type: ENHANCED
      rule:
        scan_frequency: SCAN_ON_PUSH
        repository_filter:
          filter: "*"
          filter_type: WILDCARD
      rule:
        scan_frequency: CONTINUOUS_SCAN
        repository_filter:
          filter: example
          filter_type: WILDCARD
```
