# Shield Proactive Engagement

Manage Shield Proactive Engagement resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_shield_proactive_engagement:
    example:
      enabled: true
      emergency_contact:
        contact_notes: Notes
        email_address: contact1@example.com
        phone_number: +12358132134
      emergency_contact:
        contact_notes: Notes 2
        email_address: contact2@example.com
        phone_number: +12358132134
      depends_on: 
        - ${aws_shield_drt_access_role_arn_association.example}

resource:
  aws_iam_role:
    example:
      name: example-role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Sid" : "", "Effect" : "Allow", "Principal" : { "Service" : "drt.shield.amazonaws.com" }, "Action" : "sts:AssumeRole" }, ] }'

resource:
  aws_iam_role_policy_attachment:
    example:
      role: ${aws_iam_role.example.name}
      policy_arn: "arn:aws:iam::aws:policy/service-role/AWSShieldDRTAccessPolicy"

resource:
  aws_shield_drt_access_role_arn_association:
    example:
      role_arn: ${aws_iam_role.example.arn}

resource:
  aws_shield_protection_group:
    example:
      protection_group_id: example
      aggregation: MAX
      pattern: ALL
```
