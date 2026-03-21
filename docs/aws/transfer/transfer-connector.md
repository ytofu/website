# Transfer Connector

Manage Transfer Connector resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_transfer_connector:
    example:
      access_role: ${aws_iam_role.test.arn}
      as2_config:
        compression: DISABLED
        encryption_algorithm: AWS128_CBC
        message_subject: For Connector
        local_profile_id: ${aws_transfer_profile.local.profile_id}
        mdn_response: NONE
        mdn_signing_algorithm: NONE
        partner_profile_id: ${aws_transfer_profile.partner.profile_id}
        signing_algorithm: NONE
      url: "http://www.test.com"
```

## SFTP Connector

```yaml
resource:
  aws_transfer_connector:
    example:
      access_role: ${aws_iam_role.test.arn}
      sftp_config:
        trusted_host_keys: 
          - ssh-rsa AAAAB3NYourKeysHere
        user_secret_id: ${aws_secretsmanager_secret.example.id}
      url: "sftp://test.com"
```

## SFTP Connector with VPC Lattice

```yaml
resource:
  aws_transfer_connector:
    example:
      access_role: ${aws_iam_role.test.arn}
      sftp_config:
        trusted_host_keys: 
          - ssh-rsa AAAAB3NYourKeysHere
        user_secret_id: ${aws_secretsmanager_secret.example.id}
      egress_config:
        vpc_lattice:
          resource_configuration_arn: "arn:aws:vpc-lattice:us-east-1:123456789012:resourceconfiguration/rcfg-12345678901234567"
          port_number: 22
```
