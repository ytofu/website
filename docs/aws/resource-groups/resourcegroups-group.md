# Resourcegroups Group

Manage Resourcegroups Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_resourcegroups_group:
    test:
      name: test-group
      resource_query:
        query: |
          {
          "ResourceTypeFilters": [
          "AWS::EC2::Instance"
          ],
          "TagFilters": [
          {
          "Key": "Stage",
          "Values": ["Test"]
          }
          ]
          }
```
