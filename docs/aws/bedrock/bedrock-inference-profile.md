# Resource: aws_bedrock_inference_profile

ytofu resource for managing an AWS Bedrock Inference Profile.

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

## Argument Reference

The following arguments are required:

* `name` - (Required) The name of the inference profile.
* `model_source` - (Required) The source of the model this inference profile will track metrics and cost for. See [`model_source`](#model_source).

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) The description of the inference profile.
* `tags` - (Optional) Key-value mapping of resource tags for the inference profile.

### `model_source`

- `copy_from` - The Amazon Resource Name (ARN) of the model.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

- `arn` - The Amazon Resource Name (ARN) of the inference profile.
- `id` - The unique identifier of the inference profile.
- `name` - The unique identifier of the inference profile.
- `models` - A list of information about each model in the inference profile. See [`models`](#models).
- `status` - The status of the inference profile. `ACTIVE` means that the inference profile is available to use.
- `type` - The type of the inference profile. `SYSTEM_DEFINED` means that the inference profile is defined by Amazon Bedrock. `APPLICATION` means that the inference profile is defined by the user.
- `created_at` - The time at which the inference profile was created.
- `description` - The description of the inference profile.
- `updated_at` - The time at which the inference profile was last updated.

### `models`

- `model_arn` - The Amazon Resource Name (ARN) of the model.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `update` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_bedrock_inference_profile.example inference_profile-id-12345678
```
