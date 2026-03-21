# Resource: aws_verifiedaccess_trust_provider

ytofu resource for managing a Verified Access Trust Provider.

## Basic Example

```yaml
resource:
  aws_verifiedaccess_trust_provider:
    example:
      policy_reference_name: example
      trust_provider_type: user
      user_trust_provider_type: iam-identity-center
```

## Argument Reference

The following arguments are required:

* `policy_reference_name` - (Required) The identifier to be used when working with policy rules.
* `trust_provider_type` - (Required) The type of trust provider can be either user or device-based.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) A description for the AWS Verified Access trust provider.
* `device_options` - (Optional) A block of options for device identity based trust providers.
* `device_trust_provider_type` (Optional) The type of device-based trust provider.
* `native_application_oidc_options` - (Optional) The OpenID Connect details for an Native Application OIDC, user-identity based trust provider.
* `oidc_options` - (Optional) The OpenID Connect details for an oidc-type, user-identity based trust provider.
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `user_trust_provider_type` - (Optional) The type of user-based trust provider.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the AWS Verified Access trust provider.

## Timeouts

Configuration options:

* `create` - (Default `60m`)
* `update` - (Default `180m`)
* `delete` - (Default `90m`)

## Import

```bash
ytofu import aws_verifiedaccess_trust_provider.example vatp-8012925589
```
