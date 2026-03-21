# IOT Thing Group

Manage IOT Thing Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iot_thing_group:
    parent:
      name: parent

resource:
  aws_iot_thing_group:
    example:
      name: example
      parent_group_name: ${aws_iot_thing_group.parent.name}
      properties:
        attribute_payload:
          attributes:
            One: 11111
            Two: TwoTwo
        description: This is my thing group
      tags:
        terraform: true
```
