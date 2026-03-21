# API Gateway Rest API Policy

Manage API Gateway Rest API Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    test:
      name: example-rest-api

data:
  aws_iam_policy_document:
    test:
      statement:
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "*"
        actions: 
          - "execute-api:Invoke"
        resources: 
          - "${aws_api_gateway_rest_api.test.execution_arn}/*"
        condition:
          test: IpAddress
          values: 
            - 123.123.123.123/32

resource:
  aws_api_gateway_rest_api_policy:
    test:
      rest_api_id: ${aws_api_gateway_rest_api.test.id}
      policy: ${data.aws_iam_policy_document.test.json}
```
