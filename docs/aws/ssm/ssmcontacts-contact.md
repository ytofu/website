# Ssmcontacts Contact

Manage Ssmcontacts Contact resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssmcontacts_contact:
    example:
      alias: alias
      type: PERSONAL
      depends_on: 
        - ${aws_ssmincidents_replication_set.example}
```

## Usage With All Fields

```yaml
resource:
  aws_ssmcontacts_contact:
    example:
      alias: alias
      display_name: displayName
      type: ESCALATION
      tags:
        key: value
      depends_on: 
        - ${aws_ssmincidents_replication_set.example}
```
