# Elasticache User Group

Manage Elasticache User Group resources using ytofu YAML.

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
