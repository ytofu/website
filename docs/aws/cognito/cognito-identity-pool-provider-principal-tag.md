# Resource: aws_cognito_identity_pool_provider_principal_tag

Provides an AWS Cognito Identity Principal Mapping.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: user pool
      auto_verified_attributes: 
        - email

  aws_cognito_user_pool_client:
    example:
      name: client
      user_pool_id: ${aws_cognito_user_pool.example.id}
      supported_identity_providers: []

  aws_cognito_identity_pool:
    example:
      identity_pool_name: identity pool
      allow_unauthenticated_identities: false
      cognito_identity_providers:
        client_id: ${aws_cognito_user_pool_client.example.id}
        provider_name: ${aws_cognito_user_pool.example.endpoint}
        server_side_token_check: false

  aws_cognito_identity_pool_provider_principal_tag:
    example:
      identity_pool_id: ${aws_cognito_identity_pool.example.id}
      identity_provider_name: ${aws_cognito_user_pool.example.endpoint}
      use_defaults: false
      principal_tags:
        test: value```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `identity_pool_id` (Required) - An identity pool ID.
* `identity_provider_name` (Required) - The name of the identity provider.
* `principal_tags`: (Optional: []) - String to string map of variables.
* `use_defaults`: (Optional: true) use default (username and clientID) attribute mappings.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_cognito_identity_pool_provider_principal_tag.example us-west-2_abc123:CorpAD
```
