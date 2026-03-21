# Applicationinsights Application

Manage Applicationinsights Application resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_applicationinsights_application:
    example:
      resource_group_name: ${aws_resourcegroups_group.example.name}

resource:
  aws_resourcegroups_group:
    example:
      name: example
      resource_query:
        query: '{ "ResourceTypeFilters": [ "AWS::EC2::Instance" ] "TagFilters": [ { "Key": "Stage" "Values": [ "Test" ] } ] }'
```
