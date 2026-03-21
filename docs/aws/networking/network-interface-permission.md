# Resource: aws_network_interface_permission

Grant cross-account access to an Elastic network interface (ENI).

## Basic Example

```yaml
resource:
  aws_network_interface:
    example:
      subnet_id: ${aws_subnet.example.id}
      private_ips: 
        - 10.0.0.50
      security_groups: 
        - ${aws_security_group.example.id}
      attachment:
        instance: ${aws_instance.example.id}
        device_index: 1

  aws_network_interface_permission:
    example:
      network_interface_id: ${aws_network_interface.example.id}
      aws_account_id: 123456789012
      permission: INSTANCE-ATTACH```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `network_interface_id` - (Required) The ID of the network interface.
* `aws_account_id` - (Required) The Amazon Web Services account ID.
* `permission` - (Required) The type of permission to grant. Valid values are `INSTANCE-ATTACH` or `EIP-ASSOCIATE`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `network_interface_permission_id` - ENI permission ID.

## Import

```bash
ytofu import aws_network_interface_permission.example eni-perm-056ad97ce2ac377ed
```
