# Bedrock Inference Profile

Manage Bedrock Inference Profile resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_bedrock_inference_profile:
    example:
      name: Claude Sonnet for Project 123
      description: Profile with tag for cost allocation tracking
      model_source:
        copy_from: "arn:aws:bedrock:us-west-2::foundation-model/anthropic.claude-3-5-sonnet-20241022-v2:0"
      tags:
        ProjectID: 123
```
