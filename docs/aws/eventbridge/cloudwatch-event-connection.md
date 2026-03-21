# Resource: aws_cloudwatch_event_connection

Provides an EventBridge connection resource.

## Basic Example

```yaml
resource:
  aws_cloudwatch_event_connection:
    test:
      name: ngrok-connection
      description: A connection description
      authorization_type: API_KEY
      auth_parameters:
        api_key:
          key: x-signature
          value: 1234
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name for the connection. Maximum of 64 characters consisting of numbers, lower/upper case letters, .,-,_.
* `description` - (Optional) Description for the connection. Maximum of 512 characters.
* `authorization_type` - (Required) Type of authorization to use for the connection. One of `API_KEY`,`BASIC`,`OAUTH_CLIENT_CREDENTIALS`.
* `auth_parameters` - (Required) Parameters used for authorization. A maximum of 1 are allowed. Documented below.
* `invocation_connectivity_parameters` - (Optional) Parameters to use for invoking a private API. Documented below.
* `kms_key_identifier` - (Optional) Identifier of the AWS KMS customer managed key for EventBridge to use, if you choose to use a customer managed key to encrypt this connection. The identifier can be the key Amazon Resource Name (ARN), KeyId, key alias, or key alias ARN.

`auth_parameters` support the following:

* `api_key` - (Optional) Parameters used for API_KEY authorization. An API key to include in the header for each authentication request. A maximum of 1 are allowed. Conflicts with `basic` and `oauth`. Documented below.
* `basic` - (Optional) Parameters used for BASIC authorization. A maximum of 1 are allowed. Conflicts with `api_key` and `oauth`. Documented below.
* `connectivity_parameters` - (Optional) Parameters used for `oauth` with private API. Documented below.
* `invocation_http_parameters` - (Optional) Invocation Http Parameters are additional credentials used to sign each Invocation of the ApiDestination created from this Connection. If the ApiDestination Rule Target has additional HttpParameters, the values will be merged together, with the Connection Invocation Http Parameters taking precedence. Secret values are stored and managed by AWS Secrets Manager. A maximum of 1 are allowed. Documented below.
* `oauth` - (Optional) Parameters used for OAUTH_CLIENT_CREDENTIALS authorization. A maximum of 1 are allowed. Conflicts with `basic` and `api_key`. Documented below.

`api_key` support the following:

* `key` - (Required) Header Name.
* `value` - (Required) Header Value. Created and stored in AWS Secrets Manager.

`basic` support the following:

* `username` - (Required) A username for the authorization.
* `password` - (Required) A password for the authorization. Created and stored in AWS Secrets Manager.

`oauth` support the following:

* `authorization_endpoint` - (Required) The URL to the authorization endpoint.
* `http_method` - (Required) A password for the authorization. Created and stored in AWS Secrets Manager.
* `client_parameters` - (Required) Contains the client parameters for OAuth authorization. Contains the following two parameters.
    * `client_id` - (Required) The client ID for the credentials to use for authorization. Created and stored in AWS Secrets Manager.
    * `client_secret` - (Required) The client secret for the credentials to use for authorization. Created and stored in AWS Secrets Manager.
* `oauth_http_parameters` - (Required) OAuth Http Parameters are additional credentials used to sign the request to the authorization endpoint to exchange the OAuth Client information for an access token. Secret values are stored and managed by AWS Secrets Manager. A maximum of 1 are allowed. Documented below.

`invocation_http_parameters` and `oauth_http_parameters` support the following:

* `body` - (Optional) Contains additional body string parameters for the connection. You can include up to 100 additional body string parameters per request. Each additional parameter counts towards the event payload size, which cannot exceed 64 KB. Each parameter can contain the following:
    * `key` - (Required) The key for the parameter.
    * `value` - (Required) The value associated with the key. Created and stored in AWS Secrets Manager if is secret.
    * `is_value_secret` - (Optional) Specified whether the value is secret.

* `header` - (Optional) Contains additional header parameters for the connection. You can include up to 100 additional body string parameters per request. Each additional parameter counts towards the event payload size, which cannot exceed 64 KB. Each parameter can contain the following:
    * `key` - (Required) The key for the parameter.
    * `value` - (Required) The value associated with the key. Created and stored in AWS Secrets Manager if is secret.
    * `is_value_secret` - (Optional) Specified whether the value is secret.

* `query_string` - (Optional) Contains additional query string parameters for the connection. You can include up to 100 additional body string parameters per request. Each additional parameter counts towards the event payload size, which cannot exceed 64 KB. Each parameter can contain the following:
    * `key` - (Required) The key for the parameter.
    * `value` - (Required) The value associated with the key. Created and stored in AWS Secrets Manager if is secret.
    * `is_value_secret` - (Optional) Specified whether the value is secret.

`invocation_connectivity_parameters` supports the following:

* `resource_parameters` - (Required) The parameters for EventBridge to use when invoking the resource endpoint. Documented below.

`connectivity_parameters` supports the following:

* `resource_parameters` - (Required) The parameters for EventBridge to use when invoking the authentication endpoint. Documented below.

`resource_parameters` supports the following:

* `resource_configuration_arn` - (Required) ARN of the Amazon VPC Lattice [resource configuration](vpclattice_resource_configuration) for the resource endpoint.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of the connection.
* `secret_arn` - The Amazon Resource Name (ARN) of the secret created from the authorization parameters specified for the connection.

## Import

```bash
ytofu import aws_cloudwatch_event_connection.test ngrok-connection
```
