# Connect User

Manage Connect User resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_user:
    example:
      instance_id: ${aws_connect_instance.example.id}
      name: example
      password: Password123
      routing_profile_id: ${aws_connect_routing_profile.example.routing_profile_id}
      security_profile_ids:
        - ${aws_connect_security_profile.example.security_profile_id}
      identity_info:
        first_name: example
        last_name: example2
      phone_config:
        after_contact_work_time_limit: 0
        phone_type: SOFT_PHONE
```

## With hierarchy_group_id

```yaml
resource:
  aws_connect_user:
    example:
      instance_id: ${aws_connect_instance.example.id}
      name: example
      password: Password123
      routing_profile_id: ${aws_connect_routing_profile.example.routing_profile_id}
      hierarchy_group_id: ${aws_connect_user_hierarchy_group.example.hierarchy_group_id}
      security_profile_ids:
        - ${aws_connect_security_profile.example.security_profile_id}
      identity_info:
        first_name: example
        last_name: example2
      phone_config:
        after_contact_work_time_limit: 0
        phone_type: SOFT_PHONE
```

## With identity_info filled

```yaml
resource:
  aws_connect_user:
    example:
      instance_id: ${aws_connect_instance.example.id}
      name: example
      password: Password123
      routing_profile_id: ${aws_connect_routing_profile.example.routing_profile_id}
      security_profile_ids:
        - ${aws_connect_security_profile.example.security_profile_id}
      identity_info:
        email: example@example.com
        first_name: example
        last_name: example2
        secondary_email: secondary@example.com
      phone_config:
        after_contact_work_time_limit: 0
        phone_type: SOFT_PHONE
```

## With phone_config phone type as desk phone

```yaml
resource:
  aws_connect_user:
    example:
      instance_id: ${aws_connect_instance.example.id}
      name: example
      password: Password123
      routing_profile_id: ${aws_connect_routing_profile.example.routing_profile_id}
      security_profile_ids:
        - ${aws_connect_security_profile.example.security_profile_id}
      phone_config:
        after_contact_work_time_limit: 0
        phone_type: SOFT_PHONE
```

## With multiple Security profile ids specified in security_profile_ids

```yaml
resource:
  aws_connect_user:
    example:
      instance_id: ${aws_connect_instance.example.id}
      name: example
      password: Password123
      routing_profile_id: ${aws_connect_routing_profile.example.routing_profile_id}
      security_profile_ids:
        - ${aws_connect_security_profile.example.security_profile_id}
        - ${aws_connect_security_profile.example2.security_profile_id}
      phone_config:
        after_contact_work_time_limit: 0
        auto_accept: false
        desk_phone_number: +112345678912
        phone_type: DESK_PHONE
```
