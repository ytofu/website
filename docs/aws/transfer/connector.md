# Transfer Connector

Create SFTP connectors using ytofu YAML.

## Basic SFTP Connector

```yaml
resource:
  aws_transfer_connector:
    example:
      access_role: ${aws_iam_role.transfer.arn}
      sftp_config:
        trusted_host_keys:
          - ssh-rsa AAAAB3NzaC1yc2E...
        user_secret_id: ${aws_secretsmanager_secret.sftp_creds.id}
      url: sftp://sftp.example.com
```
