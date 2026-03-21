# Resource: aws_redshift_authentication_profile

Creates a Redshift authentication profile

## Basic Example

```yaml
resource:
  aws_redshift_authentication_profile:
    example:
      authentication_profile_name: example
      authentication_profile_content: 'example-json-policy'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `authentication_profile_name` - (Required, Forces new resource) The name of the authentication profile.
* `authentication_profile_content` - (Required) The content of the authentication profile in JSON format. The maximum length of the JSON string is determined by a quota for your account.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the authentication profile.

## Import

```bash
ytofu import aws_redshift_authentication_profile.test example
```
