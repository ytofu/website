# Opensearchserverless Lifecycle Policy

Manage Opensearchserverless Lifecycle Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_opensearchserverless_lifecycle_policy:
    example:
      name: example
      type: retention
      policy: '{ "Rules" : [ { "ResourceType" : "index", "Resource" : ["index/autoparts-inventory/*"], "MinIndexRetention" : "81d" }, { "ResourceType" : "index", "Resource" : ["index/sales/orders*"], "NoMinIndexRetention" : true } ] }'
```
