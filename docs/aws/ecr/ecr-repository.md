# ECR Repository

Manage ECR Repository resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecr_repository:
    foo:
      name: bar
      image_tag_mutability: MUTABLE
      image_scanning_configuration:
        scan_on_push: true
```

## With Image Tag Mutability Exclusion

```yaml
resource:
  aws_ecr_repository:
    example:
      name: example-repo
      image_tag_mutability: IMMUTABLE_WITH_EXCLUSION
      image_tag_mutability_exclusion_filter:
        filter: "latest*"
        filter_type: WILDCARD
      image_tag_mutability_exclusion_filter:
        filter: "dev-*"
        filter_type: WILDCARD
```
