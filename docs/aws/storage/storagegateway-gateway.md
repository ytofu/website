# Storagegateway Gateway

Manage Storagegateway Gateway resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_volume_attachment:
    test:
      device_name: /dev/xvdb
      volume_id: ${aws_ebs_volume.test.id}
      instance_id: ${aws_instance.test.id}

data:
  aws_storagegateway_local_disk:
    test:
      disk_node: ${data.aws_volume_attachment.test.device_name}
      gateway_arn: ${aws_storagegateway_gateway.test.arn}

resource:
  aws_storagegateway_cache:
    test:
      disk_id: ${data.aws_storagegateway_local_disk.test.disk_id}
      gateway_arn: ${aws_storagegateway_gateway.test.arn}
```

## FSx File Gateway

```yaml
resource:
  aws_storagegateway_gateway:
    example:
      gateway_ip_address: 1.2.3.4
      gateway_name: example
      gateway_timezone: GMT
      gateway_type: FILE_FSX_SMB
      smb_active_directory_settings:
        domain_name: corp.example.com
        password: avoid-plaintext-passwords
        username: Admin
```

## S3 File Gateway

```yaml
resource:
  aws_storagegateway_gateway:
    example:
      gateway_ip_address: 1.2.3.4
      gateway_name: example
      gateway_timezone: GMT
      gateway_type: FILE_S3
```

## Tape Gateway

```yaml
resource:
  aws_storagegateway_gateway:
    example:
      gateway_ip_address: 1.2.3.4
      gateway_name: example
      gateway_timezone: GMT
      gateway_type: VTL
      medium_changer_type: AWS-Gateway-VTL
      tape_drive_type: IBM-ULT3580-TD5
```

## Volume Gateway (Cached)

```yaml
resource:
  aws_storagegateway_gateway:
    example:
      gateway_ip_address: 1.2.3.4
      gateway_name: example
      gateway_timezone: GMT
      gateway_type: CACHED
```

## Volume Gateway (Stored)

```yaml
resource:
  aws_storagegateway_gateway:
    example:
      gateway_ip_address: 1.2.3.4
      gateway_name: example
      gateway_timezone: GMT
      gateway_type: STORED
```
