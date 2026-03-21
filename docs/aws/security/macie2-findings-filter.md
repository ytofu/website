# Macie2 Findings Filter

Manage Macie2 Findings Filter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_macie2_account:
    example:

resource:
  aws_macie2_findings_filter:
    test:
      name: NAME OF THE FINDINGS FILTER
      description: DESCRIPTION
      position: 1
      action: ARCHIVE
      finding_criteria:
        criterion:
          field: region
          eq: 
            - ${data.aws_region.current.region}
      depends_on: 
        - ${aws_macie2_account.test}
```
