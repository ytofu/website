# DX Macsec Key Association

Manage DX Macsec Key Association resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_dx_connection:
    example:
      name: tf-dx-connection

resource:
  aws_dx_macsec_key_association:
    test:
      connection_id: ${data.aws_dx_connection.example.id}
      ckn: 0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef
      cak: abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789
```

## Create MACSec key with existing Secrets Manager secret

```yaml
data:
  aws_dx_connection:
    example:
      name: tf-dx-connection

data:
  aws_secretsmanager_secret:
    example:
      name: directconnect!prod/us-east-1/directconnect/0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef

resource:
  aws_dx_macsec_key_association:
    test:
      connection_id: ${data.aws_dx_connection.example.id}
      secret_arn: ${data.aws_secretsmanager_secret.example.arn}
```
