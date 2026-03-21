# Lightsail Key Pair

Manage Lightsail Key Pair resources using ytofu YAML.

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
