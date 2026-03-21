# Connect User Hierarchy Group

Manage Connect User Hierarchy Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_user_hierarchy_group:
    example:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: example
      tags: 
```

## With a parent group

```yaml
resource:
  aws_connect_user_hierarchy_group:
    parent:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: parent
      tags: 

resource:
  aws_connect_user_hierarchy_group:
    child:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: child
      parent_group_id: ${aws_connect_user_hierarchy_group.parent.hierarchy_group_id}
      tags: 
```
