# Elasticache User

Manage Elasticache User resources using ytofu YAML.

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
