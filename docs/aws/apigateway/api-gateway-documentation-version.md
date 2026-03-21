# Resource: aws_api_gateway_documentation_version

Provides a resource to manage an API Gateway Documentation Version.

## Basic Example

```yaml
resource:
  aws_api_gateway_documentation_version:
    example:
      version: example_version
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      description: Example description
      depends_on: 
        - ${aws_api_gateway_documentation_part.example}

resource:
  aws_api_gateway_rest_api:
    example:
      name: example_api

resource:
  aws_api_gateway_documentation_part:
    example:
      location:
        type: API
      properties: "{\"description\":\"Example\"}"
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `version` - (Required) Version identifier of the API documentation snapshot.
* `rest_api_id` - (Required) ID of the associated Rest API
* `description` - (Optional) Description of the API documentation version.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

## Import

```bash
ytofu import aws_api_gateway_documentation_version.example 5i4e1ko720/example-version
```
