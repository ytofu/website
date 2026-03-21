# Resource: aws_cognito_managed_login_branding

Manages branding settings for a user pool style and associates it with an app client.

## Basic Example

```yaml
resource:
  aws_cognito_managed_login_branding:
    client:
      client_id: ${aws_cognito_user_pool_client.example.id}
      user_pool_id: ${aws_cognito_user_pool.example.id}
      use_cognito_provided_values: true
```

## Custom Branding Style

```yaml
resource:
  aws_cognito_managed_login_branding:
    client:
      client_id: ${aws_cognito_user_pool_client.example.id}
      user_pool_id: ${aws_cognito_user_pool.example.id}
      asset:
        bytes: example-value
        category: PAGE_HEADER_BACKGROUND
        color_mode: DARK
        extension: SVG
      settings: '{ # Your settings here. }'
```

## Argument Reference

The following arguments are required:

* `client_id` - (Required) App client that the branding style is for.
* `user_pool_id` - (Required) User pool the client belongs to.

The following arguments are optional:

* `asset` - (Optional) Image files to apply to roles like backgrounds, logos, and icons. See [details below](#asset).
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `settings` - (Optional) JSON document with the the settings to apply to the style.
* `use_cognito_provided_values` - (Optional) When `true`, applies the default branding style options.

### asset

* `bytes` - (Optional) Image file, in Base64-encoded binary.
* `category` - (Required) Category that the image corresponds to. See [AWS documentation](https://docs.aws.amazon.com/cognito-user-identity-pools/latest/APIReference/API_AssetType.html#CognitoUserPools-Type-AssetType-Category) for valid values.
* `color_mode` - (Required) Display-mode target of the asset. Valid values: `LIGHT`, `DARK`, `DYNAMIC`.
* `extensions` - (Required) File type of the image file. See [AWS documentation](https://docs.aws.amazon.com/cognito-user-identity-pools/latest/APIReference/API_AssetType.html#CognitoUserPools-Type-AssetType-Extension) for valid values.
* `resource_id` - (Optional) Asset ID.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `managed_login_branding_id` - ID of the managed login branding style.
* `settings_all` - Settings including Amazon Cognito defaults.

## Import

```bash
ytofu import aws_cognito_managed_login_branding.example us-west-2_rSss9Zltr,06c6ae7b-1e66-46d2-87a9-1203ea3307bd
```
