# Resource: aws_api_gateway_base_path_mapping

Connects a custom domain name registered via `aws_api_gateway_domain_name`
with a deployed API so that its methods can be called via the
custom domain name.

## Basic Example

```yaml
resource:
  aws_api_gateway_stage:
    example:
      deployment_id: ${aws_api_gateway_deployment.example.id}
      rest_api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: example

resource:
  aws_api_gateway_domain_name:
    example:
      domain_name: example.com
      certificate_name: example-api
      certificate_body: file-content
      certificate_chain: file-content
      certificate_private_key: file-content

resource:
  aws_api_gateway_base_path_mapping:
    example:
      api_id: ${aws_api_gateway_rest_api.example.id}
      stage_name: ${aws_api_gateway_stage.example.stage_name}
      domain_name: ${aws_api_gateway_domain_name.example.domain_name}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `domain_name` - (Required) Already-registered domain name to connect the API to.
* `api_id` - (Required) ID of the API to connect.
* `stage_name` - (Optional) Name of a specific deployment stage to expose at the given path. If omitted, callers may select any stage by including its name as a path element after the base path.
* `base_path` - (Optional) Path segment that must be prepended to the path when accessing the API via this mapping. If omitted, the API is exposed at the root of the given domain.
* `domain_name_id` - (Optional) The identifier for the domain name resource. Supported only for private custom domain names.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_api_gateway_base_path_mapping.example example.com/
```
