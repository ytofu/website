# Resource: aws_networkmanager_connection

Manages a Network Manager Connection.

## Basic Example

```yaml
resource:
  aws_networkmanager_connection:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
      device_id: ${aws_networkmanager_device.example1.id}
      connected_device_id: ${aws_networkmanager_device.example2.id}
```

## Argument Reference

The following arguments are required:

* `connected_device_id` - (Required) ID of the second device in the connection.
* `device_id` - (Required) ID of the first device in the connection.
* `global_network_id` - (Required) ID of the global network.

The following arguments are optional:

* `connected_link_id` - (Optional) ID of the link for the second device.
* `description` - (Optional) Description of the connection.
* `link_id` - (Optional) ID of the link for the first device.
* `tags` - (Optional) Key-value tags for the connection. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the connection.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)
* `update` - (Default `10m`)

## Import

```bash
ytofu import aws_networkmanager_connection.example arn:aws:networkmanager::123456789012:device/global-network-0d47f6t230mz46dy4/connection-07f6fd08867abc123
```
