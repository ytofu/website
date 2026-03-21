# OpenSearch Serverless Collection

Create serverless collections using ytofu YAML.

## Search Collection

```yaml
resource:
  aws_opensearchserverless_collection:
    example:
      name: example
      type: SEARCH
```

## Time Series Collection

```yaml
resource:
  aws_opensearchserverless_collection:
    example:
      name: logs
      type: TIMESERIES
      depends_on:
        - aws_opensearchserverless_security_policy.encryption
```

## With Encryption Policy

```yaml
resource:
  aws_opensearchserverless_security_policy:
    encryption:
      name: example
      type: encryption
      policy: |
        {
          "Rules": [{"Resource": ["collection/example"], "ResourceType": "collection"}],
          "AWSOwnedKey": true
        }
```
