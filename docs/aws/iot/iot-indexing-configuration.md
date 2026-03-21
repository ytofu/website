# IOT Indexing Configuration

Manage IOT Indexing Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iot_indexing_configuration:
    example:
      thing_indexing_configuration:
        thing_indexing_mode: REGISTRY_AND_SHADOW
        thing_connectivity_indexing_mode: STATUS
        device_defender_indexing_mode: VIOLATIONS
        named_shadow_indexing_mode: ON
        filter:
          named_shadow_names: 
            - thing1shadow
        custom_field:
          name: shadow.desired.power
          type: Boolean
        custom_field:
          name: attributes.version
          type: Number
        custom_field:
          name: shadow.name.thing1shadow.desired.DefaultDesired
          type: String
        custom_field:
          name: deviceDefender.securityProfile1.NUMBER_VALUE_BEHAVIOR.lastViolationValue.number
          type: Number
```
