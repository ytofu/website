# Resource: aws_datazone_user_profile

ytofu resource for managing an AWS DataZone User Profile.

## Basic Example

```yaml
resource:
  aws_datazone_user_profile:
    example:
      user_identifier: ${aws_iam_user.example.arn}
      domain_identifier: ${aws_datazone_domain.example.id}
      user_type: IAM_USER
```

## Argument Reference

The following arguments are required:

* `domain_identifier` - (Required) The domain identifier.
* `user_identifier` - (Required) The user identifier.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `status` - (Optional) The user profile status.
* `user_type` - (Optional) The user type.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `details` - Details about the user profile.
* `id` - The user profile identifier.
* `type` - The user profile type.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `update` - (Default `5m`)

## Import

```bash
ytofu import aws_datazone_user_profile.example arn:aws:iam::123456789012:user/example,dzd_54nakfrg9k6suo,IAM
```
