# Resource: aws_api_gateway_resource

Provides an API Gateway Resource.

## Basic Example

```yaml
resource:
  aws_api_gateway_rest_api:
    MyDemoAPI:
      name: MyDemoAPI
      description: This is my API for demonstration purposes

resource:
  aws_api_gateway_resource:
    MyDemoResource:
      rest_api_id: ${aws_api_gateway_rest_api.MyDemoAPI.id}
      parent_id: ${aws_api_gateway_rest_api.MyDemoAPI.root_resource_id}
      path_part: mydemoresource
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `rest_api_id` - (Required) ID of the associated REST API
* `parent_id` - (Required) ID of the parent API resource
* `path_part` - (Required) Last path segment of this API resource.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Resource's identifier.
* `path` - Complete path for this API resource, including all parent paths.

## Import

```bash
ytofu import aws_api_gateway_resource.example 12345abcde/67890fghij
```
