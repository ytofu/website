# Resource: aws_networkmanager_link

Manages a Network Manager link. Use this resource to create a link for a site.

## Basic Example

```yaml
resource:
  aws_networkmanager_link:
    example:
      global_network_id: ${aws_networkmanager_global_network.example.id}
      site_id: ${aws_networkmanager_site.example.id}
      bandwidth:
        upload_speed: 10
        download_speed: 50
      provider_name: MegaCorp
```

## Argument Reference

The following arguments are required:

* `bandwidth` - (Required) Upload speed and download speed in Mbps. [See below](#bandwidth).
* `global_network_id` - (Required) ID of the global network.
* `site_id` - (Required) ID of the site.

The following arguments are optional:

* `description` - (Optional) Description of the link.
* `provider_name` - (Optional) Provider of the link.
* `tags` - (Optional) Key-value tags for the link. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `type` - (Optional) Type of the link.

### bandwidth

* `download_speed` - (Optional) Download speed in Mbps.
* `upload_speed` - (Optional) Upload speed in Mbps.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Link ARN.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)
* `update` - (Default `10m`)

## Import

```bash
ytofu import aws_networkmanager_link.example arn:aws:networkmanager::123456789012:link/global-network-0d47f6t230mz46dy4/link-444555aaabbb11223
```
