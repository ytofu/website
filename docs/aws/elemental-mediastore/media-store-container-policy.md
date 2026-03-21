# Media Store Container Policy

Manage Media Store Container Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_region:
    current:

data:
  aws_caller_identity:
    current:

resource:
  aws_media_store_container:
    example:
      name: example

data:
  aws_iam_policy_document:
    example:
      statement:
        sid: MediaStoreFullAccess
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root"
        actions: 
          - "mediastore:*"
        resources: 
          - "arn:aws:mediastore:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:container/${aws_media_store_container.example.name}/*"
        condition:
          test: Bool
          values: 
            - true

resource:
  aws_media_store_container_policy:
    example:
      container_name: ${aws_media_store_container.example.name}
      policy: ${data.aws_iam_policy_document.example.json}
```
