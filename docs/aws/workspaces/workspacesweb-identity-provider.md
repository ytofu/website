# Workspacesweb Identity Provider

Manage Workspacesweb Identity Provider resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workspacesweb_portal:
    example:
      display_name: example

resource:
  aws_workspacesweb_identity_provider:
    example:
      identity_provider_name: example-saml
      identity_provider_type: SAML
      portal_arn: ${aws_workspacesweb_portal.example.portal_arn}
      identity_provider_details:
        MetadataURL: "https://example.com/metadata"
```

## OIDC Identity Provider

```yaml
resource:
  aws_workspacesweb_portal:
    test:
      display_name: test

resource:
  aws_workspacesweb_identity_provider:
    test:
      identity_provider_name: test-updated
      identity_provider_type: OIDC
      portal_arn: ${aws_workspacesweb_portal.test.portal_arn}
      identity_provider_details:
        client_id: test-client-id
        client_secret: test-client-secret
        oidc_issuer: "https://accounts.google.com"
        attributes_request_method: POST
        authorize_scopes: openid, email
```
