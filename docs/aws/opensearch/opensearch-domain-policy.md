# Opensearch Domain Policy

Manage Opensearch Domain Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_opensearch_domain:
    example:
      domain_name: tf-test
      engine_version: OpenSearch_1.1

data:
  aws_iam_policy_document:
    main:
      statement:
        effect: Allow
        principals:
          type: "*"
          identifiers: 
            - "*"
        actions: 
          - "es:*"
        resources: 
          - "${aws_opensearch_domain.example.arn}/*"
        condition:
          test: IpAddress
          values: 
            - 127.0.0.1/32

resource:
  aws_opensearch_domain_policy:
    main:
      domain_name: ${aws_opensearch_domain.example.domain_name}
      access_policies: ${data.aws_iam_policy_document.main.json}
```
