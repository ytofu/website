# Resource: aws_api_gateway_rest_api_policy

Provides an API Gateway REST API Policy.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `rest_api_id` - (Required) ID of the REST API.
* `policy` - (Required) JSON formatted policy document that controls access to the API Gateway. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy)

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the REST API

## Import

```bash
ytofu import aws_api_gateway_rest_api_policy.example 12345abcde
```
