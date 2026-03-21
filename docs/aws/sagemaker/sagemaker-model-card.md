# Sagemaker Model Card

Manage Sagemaker Model Card resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_model_card:
    example:
      model_card_name: my-model-card
      model_card_status: Draft
      content: |
        {
        "business_details": {
        "business_problem": "Quality"
        },
        "intended_uses": {
        "intended_uses": "Testing"
        },
        "additional_information": {
        "caveats_and_recommendations": "Use this"
        }
        }
```
