# Resource: aws_cognito_user_pool_ui_customization

Provides a Cognito User Pool UI Customization resource.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example

resource:
  aws_cognito_user_pool_domain:
    example:
      domain: example
      user_pool_id: ${aws_cognito_user_pool.example.id}

resource:
  aws_cognito_user_pool_client:
    example:
      name: example
      user_pool_id: ${aws_cognito_user_pool.example.id}

resource:
  aws_cognito_user_pool_ui_customization:
    example:
      client_id: ${aws_cognito_user_pool_client.example.id}
      css: ".label-customizable {font-weight: 400;}"
      image_file: ${filebase64("logo.png")}
      user_pool_id: ${aws_cognito_user_pool_domain.example.user_pool_id}
```

## UI customization settings for all clients

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example

resource:
  aws_cognito_user_pool_domain:
    example:
      domain: example
      user_pool_id: ${aws_cognito_user_pool.example.id}

resource:
  aws_cognito_user_pool_ui_customization:
    example:
      css: ".label-customizable {font-weight: 400;}"
      image_file: ${filebase64("logo.png")}
      user_pool_id: ${aws_cognito_user_pool_domain.example.user_pool_id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `client_id` (Optional) The client ID for the client app. Defaults to `ALL`. If `ALL` is specified, the `css` and/or `image_file` settings will be used for every client that has no UI customization set previously.
* `css` (Optional) - The CSS values in the UI customization, provided as a String. At least one of `css` or `image_file` is required.
* `image_file` (Optional) - The uploaded logo image for the UI customization, provided as a base64-encoded String. Drift detection is not possible for this argument. At least one of `css` or `image_file` is required.
* `user_pool_id` (Required) - The user pool ID for the user pool.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `creation_date` - The creation date in [RFC3339 format](https://tools.ietf.org/html/rfc3339#section-5.8) for the UI customization.
* `css_version` - The CSS version number.
* `image_url` - The logo image URL for the UI customization.
* `last_modified_date` - The last-modified date in [RFC3339 format](https://tools.ietf.org/html/rfc3339#section-5.8) for the UI customization.

## Import

```bash
ytofu import aws_cognito_user_pool_ui_customization.example us-west-2_ZCTarbt5C,12bu4fuk3mlgqa2rtrujgp6egq
```
