# Resourceexplorer2 View

Manage Resourceexplorer2 View resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_resourceexplorer2_index:
    example:
      type: LOCAL

resource:
  aws_resourceexplorer2_view:
    example:
      name: exampleview
      filters:
        filter_string: "resourcetype:ec2:instance"
      included_property:
        name: tags
      depends_on: 
        - ${aws_resourceexplorer2_index.example}
```
