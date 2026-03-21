# Resource: aws_appsync_api_key

Provides an AppSync API Key.

## Basic Example

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: API_KEY
      name: example

resource:
  aws_appsync_api_key:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      expires: "2018-05-03T04:00:00Z"
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `api_id` - (Required) ID of the associated AppSync API
* `description` - (Optional) API key description. Defaults to "Managed by ytofu".
* `expires` - (Optional) RFC3339 string representation of the expiry date. Rounded down to nearest hour. By default, it is 7 days from the date of creation.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - API Key ID (Formatted as ApiId:Key)
* `key` - API key

## Import

```bash
ytofu import aws_appsync_api_key.example xxxxx:yyyyy
```
