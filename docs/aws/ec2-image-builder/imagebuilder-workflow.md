# Resource: aws_imagebuilder_workflow

ytofu resource for managing an AWS EC2 Image Builder Workflow.

## Basic Example

```yaml
resource:
  aws_imagebuilder_workflow:
    example:
      name: example
      version: 1.0.0
      type: TEST
      data: |
        name: example
        description: Workflow to test an image
        schemaVersion: 1.0
        
        parameters:
        - name: waitForActionAtEnd
        type: boolean
        
        steps:
        - name: LaunchTestInstance
        action: LaunchInstance
        onFailure: Abort
        inputs:
        waitFor: "ssmAgent"
        
        - name: TerminateTestInstance
        action: TerminateInstance
        onFailure: Continue
        inputs:
        instanceId.$: "$.stepOutputs.LaunchTestInstance.instanceId"
        
        - name: WaitForActionAtEnd
        action: WaitForAction
        if:
        booleanEquals: true
        value: "$.parameters.waitForActionAtEnd"
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the workflow.
* `type` - (Required) Type of the workflow. Valid values: `BUILD`, `TEST`.
* `version` - (Required) Version of the workflow.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `change_description` - (Optional) Change description of the workflow.
* `data` - (Optional) Inline YAML string with data of the workflow. Exactly one of `data` and `uri` can be specified.
* `description` - (Optional) Description of the workflow.
* `kms_key_id` - (Optional) Amazon Resource Name (ARN) of the Key Management Service (KMS) Key used to encrypt the workflow.
* `tags` - (Optional) Key-value map of resource tags for the workflow. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `uri` - (Optional) S3 URI with data of the workflow. Exactly one of `data` and `uri` can be specified.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Amazon Resource Name (ARN) of the workflow.
* `arn` - Amazon Resource Name (ARN) of the workflow.
* `date_created` - Date the workflow was created.
* `owner` - Owner of the workflow.

## Import

```bash
ytofu import aws_imagebuilder_workflow.example arn:aws:imagebuilder:us-east-1:aws:workflow/test/example/1.0.1/1
```
