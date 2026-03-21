# Resource: aws_storagegateway_working_storage

Manages an AWS Storage Gateway working storage.

## Basic Example

```yaml
resource:
  aws_storagegateway_working_storage:
    example:
      disk_id: ${data.aws_storagegateway_local_disk.example.id}
      gateway_arn: ${aws_storagegateway_gateway.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `disk_id` - (Required) Local disk identifier. For example, `pci-0000:03:00.0-scsi-0:0:0:0`.
* `gateway_arn` - (Required) The Amazon Resource Name (ARN) of the gateway.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Combined gateway Amazon Resource Name (ARN) and local disk identifier.

## Import

```bash
ytofu import aws_storagegateway_working_storage.example arn:aws:storagegateway:us-east-1:123456789012:gateway/sgw-12345678:pci-0000:03:00.0-scsi-0:0:0:0
```
