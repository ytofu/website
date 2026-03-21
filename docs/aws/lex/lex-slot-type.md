# Lex Slot Type

Manage Lex Slot Type resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lex_slot_type:
    flower_types:
      create_version: true
      description: Types of flowers to order
      enumeration_value:
        synonyms:
          - Lirium
          - Martagon
        value: lilies
      enumeration_value:
        synonyms:
          - Eduardoregelia
          - Podonix
        value: tulips
      name: FlowerTypes
      value_selection_strategy: ORIGINAL_VALUE
```
