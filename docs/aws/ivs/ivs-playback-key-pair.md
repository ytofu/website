# Resource: aws_ivs_playback_key_pair

ytofu resource for managing an AWS IVS (Interactive Video) Playback Key Pair.

## Basic Example

```yaml
resource:
  aws_ivs_playback_key_pair:
    example:
      public_key: file-content
```

## Argument Reference

The following arguments are required:

* `public_key` - (Required) Public portion of a customer-generated key pair. Must be an ECDSA public key in PEM format.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional) Playback Key Pair name.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Playback Key Pair.
* `fingerprint` - Key-pair identifier.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_ivs_playback_key_pair.example arn:aws:ivs:us-west-2:326937407773:playback-key/KDJRJNQhiQzA
```
