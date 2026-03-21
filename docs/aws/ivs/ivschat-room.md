# Resource: aws_ivschat_room

ytofu resource for managing an AWS IVS (Interactive Video) Chat Room.

## Basic Example

```yaml
resource:
  aws_ivschat_room:
    example:
      name: tf-room
```

## Argument Reference

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `logging_configuration_identifiers` - (Optional) List of Logging Configuration
  ARNs to attach to the room.
* `maximum_message_length` - (Optional) Maximum number of characters in a single
  message. Messages are expected to be UTF-8 encoded and this limit applies
  specifically to rune/code-point count, not number of bytes.
* `maximum_message_rate_per_second` - (Optional) Maximum number of messages per
  second that can be sent to the room (by all clients).
* `message_review_handler` - (Optional) Configuration information for optional
  review of messages.
    * `fallback_result` - (Optional) The fallback behavior (whether the message
    is allowed or denied) if the handler does not return a valid response,
    encounters an error, or times out. Valid values: `ALLOW`, `DENY`.
    * `uri` - (Optional) ARN of the lambda message review handler function.
* `name` - (Optional) Room name.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Room.
* `id` - Room ID
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `update` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_ivschat_room.example arn:aws:ivschat:us-west-2:326937407773:room/GoXEXyB4VwHb
```
