# Resource: aws_iam_openid_connect_provider

Provides an IAM OpenID Connect provider.

## Basic Example

```yaml
resource:
  aws_iam_openid_connect_provider:
    default:
      url: "https://accounts.google.com"
      client_id_list:
        - 266362248691-342342xasdasdasda-apps.googleusercontent.com
      thumbprint_list: 
        - cf23df2207d99a74fbe169e3eba035e633b65d94
```

## Without A Thumbprint

```yaml
resource:
  aws_iam_openid_connect_provider:
    default:
      url: "https://accounts.google.com"
      client_id_list:
        - 266362248691-342342xasdasdasda-apps.googleusercontent.com
```

## Argument Reference

This resource supports the following arguments:

* `url` - (Required) URL of the identity provider, corresponding to the `iss` claim.
* `client_id_list` - (Required) List of client IDs (audiences) that identify the application registered with the OpenID Connect provider. This is the value sent as the `client_id` parameter in OAuth requests.
* `thumbprint_list` - (Optional) List of server certificate thumbprints for the OpenID Connect (OIDC) identity provider's server certificate(s). For certain OIDC identity providers (e.g., Auth0, GitHub, GitLab, Google, or those using an Amazon S3-hosted JWKS endpoint), AWS relies on its own library of trusted root certificate authorities (CAs) for validation instead of using any configured thumbprints. In these cases, any configured `thumbprint_list` is retained in the configuration but not used for verification. For other IdPs, if no `thumbprint_list` is provided, IAM automatically retrieves and uses the top intermediate CA thumbprint from the OIDC IdP server certificate. However, if a `thumbprint_list` is initially configured and later removed, ytofu does not prompt IAM to retrieve a thumbprint the same way. Instead, it continues using the original thumbprint list from the initial configuration. This differs from the behavior when creating an `aws_iam_openid_connect_provider` without a `thumbprint_list`.
* `tags` - (Optional) Map of resource tags for the IAM OIDC provider. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN assigned by AWS for this provider.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_iam_openid_connect_provider.default arn:aws:iam::123456789012:oidc-provider/accounts.google.com
```
