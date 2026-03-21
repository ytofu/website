# Resource: aws_appsync_type

Provides an AppSync Type.

## Basic Example

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: API_KEY
      name: example

resource:
  aws_appsync_type:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      format: SDL
      definition: |
        type Mutation
        
        {
        putPost(id: ID!,title: String! ): Post
        
        }
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `api_id` - (Required) GraphQL API ID.
* `format` - (Required) The type format: `SDL` or `JSON`.
* `definition` - (Required) The type definition.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the type.
* `description` - The type description.
* `id` - The ID is constructed from `api-id:format:name`.
* `name` - The type name.

## Import

```bash
ytofu import aws_appsync_type.example api-id:format:name
```
