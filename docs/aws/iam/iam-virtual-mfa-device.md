# Resource: aws_iam_virtual_mfa_device

Provides an IAM Virtual MFA Device.

## Basic Example

```yaml
resource:
  aws_iam_virtual_mfa_device:
    example:
      virtual_mfa_device_name: example
```

## Argument Reference

This resource supports the following arguments:

* `virtual_mfa_device_name` - (Required) Name of the virtual MFA device. Use with path to uniquely identify a virtual MFA device.
* `path` - (Optional) Path for the virtual MFA device.
* `tags` - (Optional) Map of resource tags for the virtual mfa device. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Serial number associated with the virtual MFA device.
* `arn` - Amazon Resource Name (ARN), which is also the serial number, of the virtual MFA device.
* `base_32_string_seed` - Base32 seed defined as specified in [RFC3548](https://tools.ietf.org/html/rfc3548.txt). The `base_32_string_seed` is base64-encoded.
* `enable_date` - Date and time when the virtual MFA device was enabled.
* `qr_code_png` -  QR code PNG image that encodes `otpauth://totp/$virtualMFADeviceName@$AccountName?secret=$Base32String` where `$virtualMFADeviceName` is one of the create call arguments. `AccountName` is the user name if set (otherwise, the account ID), and `Base32String` is the seed in base32 format.
* `serial_number` - Serial number associated with the virtual MFA device.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `user_name` - Name of the IAM user associated with this virtual MFA device.

## Import

```bash
ytofu import aws_iam_virtual_mfa_device.example arn:aws:iam::123456789012:mfa/example
```
