# Resource: aws_bedrock_guardrail_version

ytofu resource for managing an AWS Bedrock Guardrail Version.

## Basic Example

```yaml
resource:
  aws_bedrock_guardrail_version:
    example:
      description: example
      guardrail_arn: ${aws_bedrock_guardrail.test.guardrail_arn}
      skip_destroy: true
```

## Argument Reference

The following arguments are required:

* `guardrail_arn` - (Required) Guardrail ARN.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the Guardrail version.
* `skip_destroy` - (Optional) Whether to retain the old version of a previously deployed Guardrail. Default is `false`

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `version` - Guardrail version.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_bedrock_guardrail_version.example arn:aws:bedrock:us-west-2:123456789012:guardrail-id-12345678,1
```
