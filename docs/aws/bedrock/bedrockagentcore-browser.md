# Bedrockagentcore Browser

Manage Bedrockagentcore Browser resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagentcore_browser:
    example:
      name: example-browser
      description: Browser for web data extraction
      network_configuration:
        network_mode: PUBLIC
```

## Browser with VPC Configuration

```yaml
resource:
  aws_bedrockagentcore_browser:
    vpc_example:
      name: vpc-browser
      description: Browser with VPC configuration
      network_configuration:
        network_mode: VPC
        vpc_config:
          security_groups: 
            - sg-12345678
          subnets: 
            - subnet-12345678
            - subnet-87654321
```

## Browser with Execution Role and Recording

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - bedrock-agentcore.amazonaws.com

resource:
  aws_iam_role:
    example:
      name: bedrock-agentcore-browser-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_s3_bucket:
    recording:
      bucket: browser-recording-bucket

resource:
  aws_bedrockagentcore_browser:
    example:
      name: example-browser
      description: Browser with recording enabled
      execution_role_arn: ${aws_iam_role.example.arn}
      network_configuration:
        network_mode: PUBLIC
      recording:
        enabled: true
        s3_location:
          bucket: ${aws_s3_bucket.recording.bucket}
          prefix: browser-sessions/
```
