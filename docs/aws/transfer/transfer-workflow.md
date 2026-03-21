# Transfer Workflow

Manage Transfer Workflow resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_transfer_workflow:
    example:
      steps:
        delete_step_details:
          name: example
          source_file_location: "$${original.file}"
        type: DELETE
```

## Multistep example

```yaml
resource:
  aws_transfer_workflow:
    example:
      steps:
        custom_step_details:
          name: example
          source_file_location: "$${original.file}"
          target: ${aws_lambda_function.example.arn}
          timeout_seconds: 60
        type: CUSTOM
      steps:
        tag_step_details:
          name: example
          source_file_location: "$${original.file}"
          tags:
            key: Name
            value: Hello World
        type: TAG
```
