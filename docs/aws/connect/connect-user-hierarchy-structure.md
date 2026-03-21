# Connect User Hierarchy Structure

Manage Connect User Hierarchy Structure resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_user_hierarchy_structure:
    example:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      hierarchy_structure:
        level_one:
          name: levelone
```

## With Five Levels

```yaml
resource:
  aws_connect_user_hierarchy_structure:
    example:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      hierarchy_structure:
        level_one:
          name: levelone
        level_two:
          name: leveltwo
        level_three:
          name: levelthree
        level_four:
          name: levelfour
        level_five:
          name: levelfive
```
