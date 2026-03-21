# Appstream User Stack Association

Manage Appstream User Stack Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appstream_stack:
    test:
      name: STACK NAME

resource:
  aws_appstream_user:
    test:
      authentication_type: USERPOOL
      user_name: EMAIL

resource:
  aws_appstream_user_stack_association:
    test:
      authentication_type: ${aws_appstream_user.test.authentication_type}
      stack_name: ${aws_appstream_stack.test.name}
      user_name: ${aws_appstream_user.test.user_name}
```
