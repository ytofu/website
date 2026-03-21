# Cloudsearch Domain Service Access Policy

Manage Cloudsearch Domain Service Access Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudsearch_domain:
    example:
      name: example-domain

data:
  aws_iam_policy_document:
    example:
      statement:
        sid: search_only
        effect: Allow
        principals:
          type: "*"
          identifiers: 
            - "*"
        actions:
          - "cloudsearch:search"
          - "cloudsearch:document"
        condition:
          test: IpAddress
          values: 
            - 192.0.2.0/32

resource:
  aws_cloudsearch_domain_service_access_policy:
    example:
      domain_name: ${aws_cloudsearch_domain.example.id}
      access_policy: ${data.aws_iam_policy_document.example.json}
```
