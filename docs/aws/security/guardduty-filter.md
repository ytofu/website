# Guardduty Filter

Manage Guardduty Filter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_guardduty_filter:
    MyFilter:
      name: MyFilter
      action: ARCHIVE
      detector_id: ${aws_guardduty_detector.example.id}
      rank: 1
      finding_criteria:
        criterion:
          field: region
          equals: 
            - eu-west-1
        criterion:
          field: service.additionalInfo.threatListName
          not_equals: 
            - some-threat
            - another-threat
        criterion:
          field: updatedAt
          greater_than: "2020-01-01T00:00:00Z"
          less_than: "2020-02-01T00:00:00Z"
        criterion:
          field: severity
          greater_than_or_equal: 4
```
