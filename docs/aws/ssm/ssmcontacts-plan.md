# Ssmcontacts Plan

Manage Ssmcontacts Plan resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssmcontacts_plan:
    example:
      contact_id: "arn:aws:ssm-contacts:us-west-2:123456789012:contact/contactalias"
      stage:
        duration_in_minutes: 1
```

## Usage with SSM Contact

```yaml
resource:
  aws_ssmcontacts_contact:
    contact:
      alias: alias
      type: PERSONAL

resource:
  aws_ssmcontacts_plan:
    plan:
      contact_id: ${aws_ssmcontacts_contact.contact.arn}
      stage:
        duration_in_minutes: 1
```

## Usage With All Fields

```yaml
resource:
  aws_ssmcontacts_contact:
    escalation_plan:
      alias: escalation-plan-alias
      type: ESCALATION

resource:
  aws_ssmcontacts_contact:
    contact_one:
      alias: alias
      type: PERSONAL

resource:
  aws_ssmcontacts_contact:
    contact_two:
      alias: alias
      type: PERSONAL

resource:
  aws_ssmcontacts_plan:
    test:
      contact_id: ${aws_ssmcontacts_contact.escalation_plan.arn}
      stage:
        duration_in_minutes: 0
        target:
          contact_target_info:
            is_essential: false
            contact_id: ${aws_ssmcontacts_contact.contact_one.arn}
        target:
          contact_target_info:
            is_essential: true
            contact_id: ${aws_ssmcontacts_contact.contact_two.arn}
        target:
          channel_target_info:
            retry_interval_in_minutes: 2
            contact_channel_id: ${aws_ssmcontacts_contact_channel.channel.arn}
```
