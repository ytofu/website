# Resource: aws_dx_gateway

Provides a Direct Connect Gateway.

## Basic Example

```yaml
resource:
  aws_dx_gateway:
    example:
      name: tf-dxg-example
      amazon_side_asn: 64512
```

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) The name of the connection.
* `amazon_side_asn` - (Required) The ASN to be configured on the Amazon side of the connection. The ASN must be in the private range of 64,512 to 65,534 or 4,200,000,000 to 4,294,967,294.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the gateway.
* `id` - The ID of the gateway.
* `owner_account_id` - AWS Account ID of the gateway.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_dx_gateway.example abcd1234-dcba-5678-be23-cdef9876ab45
```
