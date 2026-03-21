# DB Proxy Endpoint

Manage DB Proxy Endpoint resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_db_proxy_endpoint:
    example:
      db_proxy_name: ${aws_db_proxy.test.name}
      db_proxy_endpoint_name: example
      vpc_subnet_ids: ${aws_subnet.test[*].id}
      target_role: READ_ONLY
```
