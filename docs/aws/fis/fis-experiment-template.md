# FIS Experiment Template

Manage FIS Experiment Template resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_fis_experiment_template:
    example:
      description: example
      role_arn: ${aws_iam_role.example.arn}
      stop_condition:
        source: none
      action:
        name: example-action
        action_id: "aws:ec2:terminate-instances"
        target:
          key: Instances
          value: example-target
      target:
        name: example-target
        resource_type: "aws:ec2:instance"
        selection_mode: COUNT(1)
        resource_tag:
          key: env
          value: example
```
