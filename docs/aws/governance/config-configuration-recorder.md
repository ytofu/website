# Config Configuration Recorder

Manage Config Configuration Recorder resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_config_configuration_recorder:
    foo:
      name: example
      role_arn: ${aws_iam_role.r.arn}

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - config.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    r:
      name: awsconfig-example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}
```

## Exclude Resources Types Usage

```yaml
resource:
  aws_config_configuration_recorder:
    foo:
      name: example
      role_arn: ${aws_iam_role.r.arn}
      recording_group:
        all_supported: false
        exclusion_by_resource_types:
          resource_types: 
            - "AWS::EC2::Instance"
        recording_strategy:
          use_only: EXCLUSION_BY_RESOURCE_TYPES
```

## Periodic Recording

```yaml
resource:
  aws_config_configuration_recorder:
    foo:
      name: example
      role_arn: ${aws_iam_role.r.arn}
      recording_group:
        all_supported: false
        include_global_resource_types: false
        resource_types: 
          - "AWS::EC2::Instance"
          - "AWS::EC2::NetworkInterface"
      recording_mode:
        recording_frequency: CONTINUOUS
        recording_mode_override:
          description: Only record EC2 network interfaces daily
          resource_types: 
            - "AWS::EC2::NetworkInterface"
          recording_frequency: DAILY
```
