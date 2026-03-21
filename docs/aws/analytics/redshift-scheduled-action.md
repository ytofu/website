# Redshift Scheduled Action

Manage Redshift Scheduled Action resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - scheduler.redshift.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    example:
      name: redshift_scheduled_action
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        actions:
          - "redshift:PauseCluster"
          - "redshift:ResumeCluster"
          - "redshift:ResizeCluster"
        resources: 
          - "*"

resource:
  aws_iam_policy:
    example:
      name: redshift_scheduled_action
      policy: ${data.aws_iam_policy_document.example.json}

resource:
  aws_iam_role_policy_attachment:
    example:
      policy_arn: ${aws_iam_policy.example.arn}
      role: ${aws_iam_role.example.name}

resource:
  aws_redshift_scheduled_action:
    example:
      name: tf-redshift-scheduled-action
      schedule: "cron(00 23 * * ? *)"
      iam_role: ${aws_iam_role.example.arn}
      target_action:
        pause_cluster:
          cluster_identifier: tf-redshift001
```

## Resize Cluster Action

```yaml
resource:
  aws_redshift_scheduled_action:
    example:
      name: tf-redshift-scheduled-action
      schedule: "cron(00 23 * * ? *)"
      iam_role: ${aws_iam_role.example.arn}
      target_action:
        resize_cluster:
          cluster_identifier: tf-redshift001
          cluster_type: multi-node
          node_type: dc1.large
          number_of_nodes: 2
```
