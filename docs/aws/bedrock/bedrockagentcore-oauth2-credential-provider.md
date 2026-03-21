# Bedrockagentcore Oauth2 Credential Provider

Manage Bedrockagentcore Oauth2 Credential Provider resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagentcore_oauth2_credential_provider:
    github:
      name: github-oauth-provider
      credential_provider_vendor: GithubOauth2
      oauth2_provider_config:
        github_oauth2_provider_config:
          client_id: your-github-client-id
          client_secret: your-github-client-secret
```

## Custom OAuth Provider with Discovery URL

```yaml
resource:
  aws_bedrockagentcore_oauth2_credential_provider:
    auth0:
      name: auth0-oauth-provider
      credential_provider_vendor: CustomOauth2
      custom_oauth2_provider_config:
        custom:
          client_id_wo: auth0-client-id
          client_secret_wo: auth0-client-secret
          client_credentials_wo_version: 1
          oauth_discovery:
            discovery_url: "https://dev-company.auth0.com/.well-known/openid-configuration"
```

## Custom OAuth Provider with Authorization Server Metadata

```yaml
resource:
  aws_bedrockagentcore_oauth2_credential_provider:
    keycloak:
      name: keycloak-oauth-provider
      credential_provider_vendor: CustomOauth2
      oauth2_provider_config:
        custom_oauth2_provider_config:
          client_id_wo: keycloak-client-id
          client_secret_wo: keycloak-client-secret
          client_credentials_wo_version: 1
          oauth_discovery:
            authorization_server_metadata:
              issuer: "https://auth.company.com/realms/production"
              authorization_endpoint: "https://auth.company.com/realms/production/protocol/openid-connect/auth"
              token_endpoint: "https://auth.company.com/realms/production/protocol/openid-connect/token"
              response_types: 
                - code
                - id_token
```
