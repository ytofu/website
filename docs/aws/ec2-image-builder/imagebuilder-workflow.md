# Imagebuilder Workflow

Manage Imagebuilder Workflow resources using ytofu YAML.

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
