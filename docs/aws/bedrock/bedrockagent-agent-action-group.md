# Bedrockagent Agent Action Group

Manage Bedrockagent Agent Action Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagent_agent_action_group:
    example:
      action_group_name: example
      agent_id: GGRRAED6JP
      agent_version: DRAFT
      skip_resource_in_use_check: true
      action_group_executor:
        lambda: "arn:aws:lambda:us-west-2:123456789012:function:example-function"
      api_schema:
        payload: file-content
```

## API Schema in S3 Bucket

```yaml
resource:
  aws_bedrockagent_agent_action_group:
    example:
      action_group_name: example
      agent_id: GGRRAED6JP
      agent_version: DRAFT
      skip_resource_in_use_check: true
      action_group_executor:
        lambda: "arn:aws:lambda:us-west-2:123456789012:function:example-function"
      api_schema:
        s3:
          s3_bucket_name: example-bucket
          s3_object_key: path/to/schema.json
```

## Function Schema (Simplified Schema)

```yaml
resource:
  aws_bedrockagent_agent_action_group:
    example:
      action_group_name: example
      agent_id: GGRRAED6JP
      agent_version: DRAFT
      skip_resource_in_use_check: true
      action_group_executor:
        lambda: "arn:aws:lambda:us-west-2:123456789012:function:example-function"
      function_schema:
        member_functions:
          functions:
            name: example-function
            description: Example function
            parameters:
              map_block_key: param1
              type: string
              description: The first parameter
              required: true
            parameters:
              map_block_key: param2
              type: integer
              description: The second parameter
              required: false
```

## Return of Control

```yaml
resource:
  aws_bedrockagent_agent_action_group:
    example:
      action_group_name: example
      agent_id: GGRRAED6JP
      agent_version: DRAFT
      skip_resource_in_use_check: true
      action_group_executor:
        custom_control: RETURN_CONTROL
      api_schema:
        payload: file-content
```
