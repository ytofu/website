# Resource: aws_networkmanager_site

Manages a Network Manager site. Use this resource to create a site in a global network.

## Basic Example

```yaml
resource:
  aws_networkmanager_global_network:
    example:

resource:
  aws_networkmanager_site:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
```

## Argument Reference

The following arguments are required:

* `global_network_id` - (Required) ID of the Global Network to create the site in.

The following arguments are optional:

* `description` - (Optional) Description of the Site.
* `location` - (Optional) Site location. [See below](#location).
* `tags` - (Optional) Key-value tags for the Site. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### location

* `address` - (Optional) Address of the location.
* `latitude` - (Optional) Latitude of the location.
* `longitude` - (Optional) Longitude of the location.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Site ARN.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)
* `update` - (Default `10m`)

## Import

```bash
ytofu import aws_networkmanager_site.example arn:aws:networkmanager::123456789012:site/global-network-0d47f6t230mz46dy4/site-444555aaabbb11223
```
