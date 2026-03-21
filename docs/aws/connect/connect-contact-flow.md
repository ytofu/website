# Connect Contact Flow

Manage Connect Contact Flow resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_contact_flow:
    test:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: Test
      description: Test Contact Flow Description
      type: CONTACT_FLOW
      content: '{ "Version": "2019-10-30" "StartAction": "12345678-1234-1234-1234-123456789012" "Actions": [ { "Identifier": "12345678-1234-1234-1234-123456789012" "Type": "MessageParticipant" "Transitions": { "NextAction": "abcdef-abcd-abcd-abcd-abcdefghijkl" "Errors": [] "Conditions": [] } "Parameters": { "Text": "Thanks for calling the sample flow!" } }, { "Identifier": "abcdef-abcd-abcd-abcd-abcdefghijkl" "Type": "DisconnectParticipant" "Transitions": {} "Parameters": {} } ] }'
      tags: 
```

## With External Content

```yaml
resource:
  aws_connect_contact_flow:
    test:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: Test
      description: Test Contact Flow Description
      type: CONTACT_FLOW
      filename: contact_flow.json
      content_hash: example-value
      tags: 
```
