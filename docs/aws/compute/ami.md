# AMI

Manage AMI resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ami:
    example:
      name: terraform-example
      virtualization_type: hvm
      root_device_name: /dev/xvda
      imds_support: "v2.0" # Enforce usage of IMDSv2. You can safely remove this line if your application explicitly doesn't support it.
      ebs_block_device:
        device_name: /dev/xvda
        snapshot_id: snap-xxxxxxxx
        volume_size: 8
```
