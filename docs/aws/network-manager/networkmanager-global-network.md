# Resource: aws_networkmanager_global_network

Manages a Network Manager Global Network.

## Basic Example

```yaml
resource:
  aws_networkmanager_global_network:
    example:
      description: example
```

## Argument Reference

The following arguments are optional:

* `description` - (Optional) Description of the Global Network.
* `tags` - (Optional) Key-value tags for the Global Network. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Global Network ARN.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)
* `update` - (Default `10m`)

## Import

```bash
ytofu import aws_networkmanager_global_network.example global-network-0d47f6t230mz46dy4
```
