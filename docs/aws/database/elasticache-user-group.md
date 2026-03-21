# Resource: aws_elasticache_user_group

Provides an ElastiCache user group resource.

## Basic Example

```yaml
resource:
  aws_elasticache_user:
    test:
      user_id: testUserId
      user_name: default
      access_string: "on ~app::* -@all +@read +@hash +@bitmap +@geo -setbit -bitfield -hset -hsetnx -hmset -hincrby -hincrbyfloat -hdel -bitop -geoadd -georadius -georadiusbymember"
      engine: redis
      passwords: 
        - password123456789

resource:
  aws_elasticache_user_group:
    test:
      engine: redis
      user_group_id: userGroupId
      user_ids: 
        - ${aws_elasticache_user.test.user_id}
```

## Argument Reference

The following arguments are required:

* `engine` - (Required) The current supported value are `redis`, `valkey` (case insensitive).
* `user_group_id` - (Required) The ID of the user group.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `user_ids` - (Optional) The list of user IDs that belong to the user group.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The user group identifier.
* `arn` - The ARN that identifies the user group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_elasticache_user_group.my_user_group userGoupId1
```
