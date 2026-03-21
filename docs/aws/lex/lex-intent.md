# Lex Intent

Manage Lex Intent resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lex_intent:
    order_flowers_intent:
      confirmation_prompt:
        max_attempts: 2
        message:
          content: "Okay, your {FlowerType} will be ready for pickup by {PickupTime} on {PickupDate}.  Does this sound okay?"
          content_type: PlainText
      create_version: false
      name: OrderFlowers
      description: Intent to order a bouquet of flowers for pick up
      fulfillment_activity:
        type: ReturnIntent
      rejection_statement:
        message:
          content: Okay, I will not place your order.
          content_type: PlainText
      sample_utterances:
        - I would like to order some flowers
        - I would like to pick up flowers
      slot:
        description: The type of flowers to pick up
        name: FlowerType
        priority: 1
        sample_utterances:
          - "I would like to order {FlowerType}"
        slot_constraint: Required
        slot_type: FlowerTypes
        slot_type_version: $$LATEST
        value_elicitation_prompt:
          max_attempts: 2
          message:
            content: What type of flowers would you like to order?
            content_type: PlainText
      slot:
        description: The date to pick up the flowers
        name: PickupDate
        priority: 2
        sample_utterances:
          - "I would like to order {FlowerType}"
        slot_constraint: Required
        slot_type: AMAZON.DATE
        slot_type_version: $$LATEST
        value_elicitation_prompt:
          max_attempts: 2
          message:
            content: "What day do you want the {FlowerType} to be picked up?"
            content_type: PlainText
      slot:
        description: The time to pick up the flowers
        name: PickupTime
        priority: 3
        sample_utterances:
          - "I would like to order {FlowerType}"
        slot_constraint: Required
        slot_type: AMAZON.TIME
        slot_type_version: $$LATEST
        value_elicitation_prompt:
          max_attempts: 2
          message:
            content: "Pick up the {FlowerType} at what time on {PickupDate}?"
            content_type: PlainText
```
