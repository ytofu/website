# Resource: aws_connect_contact_flow_module

Provides an Amazon Connect Contact Flow Module resource. For more information see
[Amazon Connect: Getting Started](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-get-started.html)

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `content` - (Optional) Specifies the content of the Contact Flow Module, provided as a JSON string, written in Amazon Connect Contact Flow Language. If defined, the `filename` argument cannot be used.
* `content_hash` - (Optional) Used to trigger updates. Must be set to a base64-encoded SHA256 hash of the Contact Flow Module source specified with `filename`. The usual way to set this is filebase64sha256("contact_flow_module.json") (ytofu 0.11.12 and later) or base64sha256(file("contact_flow_module.json")) (ytofu 0.11.11 and earlier), where "contact_flow_module.json" is the local filename of the Contact Flow Module source.
* `description` - (Optional) Specifies the description of the Contact Flow Module.
* `filename` - (Optional) The path to the Contact Flow Module source within the local filesystem. Conflicts with `content`.
* `instance_id` - (Required) Specifies the identifier of the hosting Amazon Connect Instance.
* `name` - (Required) Specifies the name of the Contact Flow Module.
* `tags` - (Optional) Tags to apply to the Contact Flow Module. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of the Contact Flow Module.
* `id` - The identifier of the hosting Amazon Connect Instance and identifier of the Contact Flow Module separated by a colon (`:`).
* `contact_flow_module_id` - The identifier of the Contact Flow Module.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_connect_contact_flow_module.example f1288a1f-6193-445a-b47e-af739b2:c1d4e5f6-1b3c-1b3c-1b3c-c1d4e5f6c1d4e5
```
