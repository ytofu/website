# Resource: aws_ssoadmin_instance_access_control_attributes

Provides a Single Sign-On (SSO) ABAC Resource: https://docs.aws.amazon.com/singlesignon/latest/userguide/abac.html

## Basic Example

```yaml
data:
  aws_ssoadmin_instances:
    example:

resource:
  aws_ssoadmin_instance_access_control_attributes:
    example:
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      attribute:
        key: name
        value:
          source: 
            - "$${path:name.givenName}"
      attribute:
        key: last
        value:
          source: 
            - "$${path:name.familyName}"
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `instance_arn` - (Required, Forces new resource) The Amazon Resource Name (ARN) of the SSO Instance.
* `attribute` - (Required) See [AccessControlAttribute](#accesscontrolattribute) for more details.

### AccessControlAttribute

* `key` - (Required) The name of the attribute associated with your identities in your identity source. This is used to map a specified attribute in your identity source with an attribute in AWS SSO.
* `value` - (Required) The value used for mapping a specified attribute to an identity source. See [AccessControlAttributeValue](#accesscontrolattributevalue)

### AccessControlAttributeValue

* `source` - (Required) The identity source to use when mapping a specified attribute to AWS SSO.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The identifier of the Instance Access Control Attribute `instance_arn`.

## Import

```bash
ytofu import aws_ssoadmin_instance_access_control_attributes.example arn:aws:sso:::instance/ssoins-0123456789abcdef
```
