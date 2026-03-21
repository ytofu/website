# Resource: aws_elasticache_user

Provides an ElastiCache user resource.

## Basic Example

```yaml
resource:
  aws_elasticache_user:
    test:
      user_id: testUserId
      user_name: testUserName
      access_string: "on ~app::* -@all +@read +@hash +@bitmap +@geo -setbit -bitfield -hset -hsetnx -hmset -hincrby -hincrbyfloat -hdel -bitop -geoadd -georadius -georadiusbymember"
      engine: redis
      passwords: 
        - password123456789
```

## Argument Reference

The following arguments are required:

* `access_string` - (Required) Access permissions string used for this user. See [Specifying Permissions Using an Access String](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/Clusters.RBAC.html#Access-string) for more details.
* `engine` - (Required) The current supported values are `redis`, `valkey` (case insensitive).
* `user_id` - (Required) The ID of the user.
* `user_name` - (Required) The username of the user.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `authentication_mode` - (Optional) Denotes the user's authentication properties. Detailed below.
* `no_password_required` - (Optional) Indicates a password is not required for this user.
* `passwords` - (Optional) Passwords used for this user. You can create up to two passwords for each user.
* `tags` - (Optional) A list of tags to be added to this resource. A tag is a key-value pair.

### authentication_mode Configuration Block

* `passwords` - (Optional) Specifies the passwords to use for authentication if `type` is set to `password`.
* `type` - (Required) Specifies the authentication type. Possible options are: `password`, `no-password-required` or `iam`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the created ElastiCache User.

## Timeouts

Configuration options:

- `create` - (Default `5m`)
- `read` - (Default `5m`)
- `update` - (Default `5m`)
- `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_elasticache_user.my_user userId1
```
