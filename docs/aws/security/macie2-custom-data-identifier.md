# Macie2 Custom Data Identifier

Manage Macie2 Custom Data Identifier resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_macie2_account:
    example:

resource:
  aws_macie2_custom_data_identifier:
    example:
      name: NAME OF CUSTOM DATA IDENTIFIER
      regex: "[0-9]{3}-[0-9]{2}-[0-9]{4}"
      description: DESCRIPTION
      maximum_match_distance: 10
      keywords: 
        - keyword
      ignore_words: 
        - ignore
      depends_on: 
        - ${aws_macie2_account.test}
```
