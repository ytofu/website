# Cognito Identity Provider

Add social and SAML identity providers to user pools using ytofu YAML.

## Google Provider

```yaml
resource:
  aws_cognito_identity_provider:
    google:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      provider_name: Google
      provider_type: Google
      provider_details:
        authorize_scopes: email
        client_id: your-client-id
        client_secret: your-client-secret
      attribute_mapping:
        email: email
        username: sub
```

## Facebook Provider

```yaml
resource:
  aws_cognito_identity_provider:
    facebook:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      provider_name: Facebook
      provider_type: Facebook
      provider_details:
        authorize_scopes: email,public_profile
        client_id: your-app-id
        client_secret: your-app-secret
        api_version: v12.0
      attribute_mapping:
        email: email
        username: id
```

## SAML Provider

```yaml
resource:
  aws_cognito_identity_provider:
    saml:
      user_pool_id: ${aws_cognito_user_pool.example.id}
      provider_name: Okta
      provider_type: SAML
      provider_details:
        MetadataURL: https://myokta.okta.com/app/exk1234567890/sso/saml/metadata
      attribute_mapping:
        email: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress
```
