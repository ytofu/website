# Resource: aws_opensearchserverless_security_config

ytofu resource for managing an AWS OpenSearch Serverless Security Config.

## Basic Example

```yaml
resource:
  aws_opensearchserverless_security_config:
    example:
      name: example
      type: saml
      saml_options:
        metadata: file-content
```

## Argument Reference

The following arguments are required:

* `name` - (Required, Forces new resource) Name of the policy.
* `saml_options` - (Required) Configuration block for SAML options.
* `type` - (Required) Type of configuration. Must be `saml`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the security configuration.

### saml_options

* `group_attribute` - (Optional) Group attribute for this SAML integration.
* `metadata` - (Required) The XML IdP metadata file generated from your identity provider.
* `session_timeout` - (Optional) Session timeout, in minutes. Minimum is 5 minutes and maximum is 720 minutes (12 hours). Default is 60 minutes.
* `user_attribute` - (Optional) User attribute for this SAML integration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `config_version` - Version of the configuration.

## Import

```bash
ytofu import aws_opensearchserverless_security_config.example saml/123456789012/example
```
