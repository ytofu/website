# Resource: aws_cloudfront_anycast_ip_list

ytofu resource for managing a CloudFront Anycast IP List.

## Basic Example

```yaml
resource:
  aws_cloudfront_anycast_ip_list:
    example:
      name: example-list
      ip_count: 21
```

## Argument Reference

The following arguments are required:

* `ip_count` - (Required, Forces new resource) The number of static IP addresses that are allocated to the Anycast IP list. Valid values: `3`, `21`.
* `name` - (Required, Forces new resource) Name of the Anycast IP list.

The following arguments are optional:

* `tags` - (Optional) Key-value tags for the place index. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `anycast_ips` - The static IP addresses that are allocated to the Anycast IP list.
* `arn` - The Anycast IP list ARN.
* `etag` - The current version of the Anycast IP list.
* `id` - The Anycast IP list ID.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_cloudfront_anycast_ip_list.example abcd-1234
```
