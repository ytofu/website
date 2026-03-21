# Verifiedpermissions Identity Source

Manage Verifiedpermissions Identity Source resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_verifiedpermissions_policy_store:
    example:
      validation_settings:
        mode: STRICT

resource:
  aws_cognito_user_pool:
    example:
      name: example

resource:
  aws_cognito_user_pool_client:
    example:
      name: example
      user_pool_id: ${aws_cognito_user_pool.example.id}
      explicit_auth_flows: 
        - ADMIN_NO_SRP_AUTH

resource:
  aws_verifiedpermissions_identity_source:
    example:
      policy_store_id: ${aws_verifiedpermissions_policy_store.example.id}
      configuration:
        cognito_user_pool_configuration:
          user_pool_arn: ${aws_cognito_user_pool.example.arn}
          client_ids: 
            - ${aws_cognito_user_pool_client.example.id}
```

## OpenID Connect Configuration Usage

```yaml
resource:
  aws_verifiedpermissions_policy_store:
    example:
      validation_settings:
        mode: STRICT

resource:
  aws_verifiedpermissions_identity_source:
    example:
      policy_store_id: ${aws_verifiedpermissions_policy_store.example.id}
      configuration:
        open_id_connect_configuration:
          issuer: "https://auth.example.com"
          token_selection:
            access_token_only:
              audiences: 
                - "https://myapp.example.com"
              principal_id_claim: sub
          entity_id_prefix: MyOIDCProvider
          group_configuration:
            group_claim: groups
            group_entity_type: "MyCorp::UserGroup"
      principal_entity_type: "MyCorp::User"
```
