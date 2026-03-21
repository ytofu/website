# Connect Contact Flow Module

Manage Connect Contact Flow Module resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_contact_flow_module:
    example:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: Example
      description: Example Contact Flow Module Description
      content: '{ "Version": "2019-10-30" "StartAction": "12345678-1234-1234-1234-123456789012" "Actions": [ { "Identifier": "12345678-1234-1234-1234-123456789012" "Parameters": { "Text": "Hello contact flow module" } "Transitions": { "NextAction": "abcdef-abcd-abcd-abcd-abcdefghijkl" "Errors": [] "Conditions": [] } "Type": "MessageParticipant" }, { "Identifier": "abcdef-abcd-abcd-abcd-abcdefghijkl" "Type": "DisconnectParticipant" "Parameters": {} "Transitions": {} } ] "Settings": { "InputParameters": [] "OutputParameters": [] "Transitions": [ { "DisplayName": "Success" "ReferenceName": "Success" "Description": "" }, { "DisplayName": "Error" "ReferenceName": "Error" "Description": "" } ] } }'
      tags: 
```

## With External Content

```yaml
resource:
  aws_connect_contact_flow_module:
    example:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: Example
      description: Example Contact Flow Module Description
      filename: contact_flow_module.json
      content_hash: example-value
      tags: 
```
