# Resource: aws_sagemaker_model_card

Manage an Amazon SageMaker Model Card.

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

## Argument Reference

This resource supports the following arguments:

* `content` - (Required) Content of the model card in [model card JSON schema](https://docs.aws.amazon.com/sagemaker/latest/dg/model-cards.html#model-cards-json-schema).
* `model_card_name` - (Required) Name of the model card.
* `model_card_status` - (Required) Approval status of the model card. Valid values: `Draft`, `PendingReview`, `Approved`, `Archived`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `security_config` - (Optional) KMS key to encrypt, decrypt, and re-encrypt model card content. Fields are documented below.
* `tags` - (Optional) A mapping of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### security_config

* `kms_key_id` - (Required) KMS key ARN.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `model_card_arn` - The Amazon Resource Name (ARN) of the model card.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `delete` - (Default `15m`)

## Import

```bash
ytofu import aws_sagemaker_model_card.example my-model-card
```
