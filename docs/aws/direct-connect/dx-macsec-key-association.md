# Resource: aws_dx_macsec_key_association

Provides a MAC Security (MACSec) secret key resource for use with Direct Connect. See [MACsec prerequisites](https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-mac-sec-getting-started.html#mac-sec-prerequisites) for information about MAC Security (MACsec) prerequisites.

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

  aws_secretsmanager_secret:
    example:
      name: directconnect!prod/us-east-1/directconnect/0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef

resource:
  aws_dx_macsec_key_association:
    test:
      connection_id: ${data.aws_dx_connection.example.id}
      secret_arn: ${data.aws_secretsmanager_secret.example.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cak` - (Optional) The MAC Security (MACsec) CAK to associate with the dedicated connection. The valid values are 64 hexadecimal characters (0-9, A-E). Required if using `ckn`.
* `ckn` - (Optional) The MAC Security (MACsec) CKN to associate with the dedicated connection. The valid values are 64 hexadecimal characters (0-9, A-E). Required if using `cak`.
* `connection_id` - (Required) The ID of the dedicated Direct Connect connection. The connection must be a dedicated connection in the `AVAILABLE` state.
* `secret_arn` - (Optional) The Amazon Resource Name (ARN) of the MAC Security (MACsec) secret key to associate with the dedicated connection.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the MAC Security (MACSec) secret key resource.
* `start_on` - The date in UTC format that the MAC Security (MACsec) secret key takes effect.
* `state` -  The state of the MAC Security (MACsec) secret key. The possible values are: associating, associated, disassociating, disassociated. See [MacSecKey](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_MacSecKey.html#DX-Type-MacSecKey-state) for descriptions of each state.
