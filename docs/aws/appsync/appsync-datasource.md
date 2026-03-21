# Appsync Datasource

Manage Appsync Datasource resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dynamodb_table:
    example:
      name: example
      read_capacity: 1
      write_capacity: 1
      hash_key: UserId
      attribute:
        name: UserId
        type: S

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - appsync.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    example:
      name: example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        actions: 
          - "dynamodb:*"
        resources: 
          - ${aws_dynamodb_table.example.arn}

resource:
  aws_iam_role_policy:
    example:
      name: example
      role: ${aws_iam_role.example.id}
      policy: ${data.aws_iam_policy_document.example.json}

resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: API_KEY
      name: tf_appsync_example

resource:
  aws_appsync_datasource:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      name: tf_appsync_example
      service_role_arn: ${aws_iam_role.example.arn}
      type: AMAZON_DYNAMODB
      dynamodb_config:
        table_name: ${aws_dynamodb_table.example.name}
```
