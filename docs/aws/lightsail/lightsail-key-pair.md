# Resource: aws_lightsail_key_pair

Manages a Lightsail Key Pair for use with Lightsail Instances. Use this resource to create or import key pairs that are separate from EC2 Key Pairs and required for Lightsail instances.

## Basic Example

```yaml
resource:
  aws_lightsail_key_pair:
    example:
      name: example
```

## Create New Key Pair with PGP Encrypted Private Key

```yaml
resource:
  aws_lightsail_key_pair:
    example:
      name: example
      pgp_key: "keybase:keybaseusername"
```

## Existing Public Key Import

```yaml
resource:
  aws_lightsail_key_pair:
    example:
      name: example
      public_key: file-content
```

## Argument Reference

The following arguments are optional:

* `name` - (Optional) Name of the Lightsail Key Pair. If omitted, ytofu will assign a random, unique name. Conflicts with `name_prefix`.
* `name_prefix` - (Optional) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `pgp_key` - (Optional) PGP key to encrypt the resulting private key material. Only used when creating a new key pair.
* `public_key` - (Optional) Public key material. This public key will be imported into Lightsail.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Map of tags to assign to the resource. To create a key-only tag, use an empty string as the value. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Lightsail key pair.
* `encrypted_fingerprint` - MD5 public key fingerprint for the encrypted private key.
* `encrypted_private_key` - Private key material, base 64 encoded and encrypted with the given `pgp_key`. This is only populated when creating a new key and `pgp_key` is supplied.
* `fingerprint` - MD5 public key fingerprint as specified in section 4 of RFC 4716.
* `id` - Name used for this key pair.
* `private_key` - Private key, base64 encoded. This is only populated when creating a new key, and when no `pgp_key` is provided.
* `public_key` - Public key, base64 encoded.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
