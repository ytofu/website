# Gamelift Game Server Group

Manage Gamelift Game Server Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_gamelift_game_server_group:
    example:
      game_server_group_name: example
      instance_definition:
        instance_type: c5.large
      instance_definition:
        instance_type: c5a.large
      launch_template:
        id: ${aws_launch_template.example.id}
      max_size: 1
      min_size: 1
      role_arn: ${aws_iam_role.example.arn}
      depends_on:
        - ${aws_iam_role_policy_attachment.example}
```

## Example IAM Role for GameLift Game Server Group

```yaml
data:
  aws_partition:
    current:

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers:
            - autoscaling.amazonaws.com
            - gamelift.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    example:
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}
      name: gamelift-game-server-group-example

resource:
  aws_iam_role_policy_attachment:
    example:
      policy_arn: "arn:${data.aws_partition.current.partition}:iam::aws:policy/GameLiftGameServerGroupPolicy"
      role: ${aws_iam_role.example.name}
```
