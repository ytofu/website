# Transfer Server

Create SFTP/FTPS/FTP servers using ytofu YAML.

## Public SFTP Server

```yaml
resource:
  aws_transfer_server:
    example:
      identity_provider_type: SERVICE_MANAGED
      protocols:
        - SFTP
      endpoint_type: PUBLIC
      tags:
        Name: example-sftp-server
```

## VPC Endpoint Server

```yaml
resource:
  aws_transfer_server:
    example:
      endpoint_type: VPC
      endpoint_details:
        subnet_ids:
          - ${aws_subnet.example.id}
        vpc_id: ${aws_vpc.example.id}
        security_group_ids:
          - ${aws_security_group.example.id}
      protocols:
        - SFTP
      identity_provider_type: SERVICE_MANAGED
```

## With Custom Domain

```yaml
resource:
  aws_transfer_server:
    example:
      protocols:
        - SFTP
      certificate: ${aws_acm_certificate.example.arn}
      identity_provider_type: SERVICE_MANAGED
      domain: S3
```

## With Logging

```yaml
resource:
  aws_transfer_server:
    example:
      protocols:
        - SFTP
      identity_provider_type: SERVICE_MANAGED
      logging_role: ${aws_iam_role.transfer_logging.arn}
      structured_log_destinations:
        - ${aws_cloudwatch_log_group.transfer.arn}:*
```
