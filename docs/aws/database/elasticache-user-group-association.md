# Resource: aws_elasticache_user_group_association

Associate an existing ElastiCache user and an existing user group.

## Basic Example

```yaml
resource:
  aws_elasticache_user:
    default:
      user_id: defaultUserID
      user_name: default
      access_string: "on ~app::* -@all +@read +@hash +@bitmap +@geo -setbit -bitfield -hset -hsetnx -hmset -hincrby -hincrbyfloat -hdel -bitop -geoadd -georadius -georadiusbymember"
      engine: REDIS
      passwords: 
        - password123456789

resource:
  aws_elasticache_user_group:
    example:
      engine: REDIS
      user_group_id: userGroupId
      user_ids: 
        - ${aws_elasticache_user.default.user_id}
      lifecycle:
        ignore_changes: 
          - user_ids

resource:
  aws_elasticache_user:
    example:
      user_id: exampleUserID
      user_name: exampleuser
      access_string: "on ~app::* -@all +@read +@hash +@bitmap +@geo -setbit -bitfield -hset -hsetnx -hmset -hincrby -hincrbyfloat -hdel -bitop -geoadd -georadius -georadiusbymember"
      engine: REDIS
      passwords: 
        - password123456789

resource:
  aws_elasticache_user_group_association:
    example:
      user_group_id: ${aws_elasticache_user_group.example.user_group_id}
      user_id: ${aws_elasticache_user.example.user_id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `user_group_id` - (Required) ID of the user group.
* `user_id` - (Required) ID of the user to associated with the user group.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_elasticache_user_group_association.example userGoupId1,userId
```
