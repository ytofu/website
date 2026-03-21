# Resource: aws_memorydb_user

Provides a MemoryDB User.

## Basic Example

```yaml
resource:
  random_password:
    example:
      length: 16

resource:
  aws_memorydb_user:
    example:
      user_name: my-user
      access_string: "on ~* &* +@all"
      authentication_mode:
        type: password
        passwords: 
          - ${random_password.example.result}
```

## Argument Reference

The following arguments are required:

* `access_string` - (Required) Access permissions string used for this user.
* `authentication_mode` - (Required) Denotes the user's authentication properties. Detailed below.
* `user_name` - (Required, Forces new resource) Name of the MemoryDB user. Up to 40 characters.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### authentication_mode Configuration Block

* `passwords` - (Optional) Set of passwords used for authentication if `type` is set to `password`. You can create up to two passwords for each user.
* `type` - (Required) Specifies the authentication type. Valid values are: `password` or `iam`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Same as `user_name`.
* `arn` - ARN of the user.
* `minimum_engine_version` - Minimum engine version supported for the user.
* `authentication_mode` configuration block
    * `password_count` - Number of passwords belonging to the user if `type` is set to `password`.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_memorydb_user.example my-user
```
