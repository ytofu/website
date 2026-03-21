# Resource: aws_network_interface_attachment

Attach an Elastic network interface (ENI) resource with EC2 instance.

## Basic Example

```yaml
resource:
  aws_network_interface_attachment:
    test:
      instance_id: ${aws_instance.test.id}
      network_interface_id: ${aws_network_interface.test.id}
      device_index: 0
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `instance_id` - (Required) Instance ID to attach.
* `network_interface_id` - (Required) ENI ID to attach.
* `device_index` - (Required) Network interface index (int).
* `network_card_index` - (Optional) Index of the network card. Specify a value greater than 0 when using multiple network cards, which are supported by [some instance types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html#network-cards). The default is 0.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `instance_id` - Instance ID.
* `network_interface_id` - Network interface ID.
* `attachment_id` - The ENI Attachment ID.
* `status` - The status of the Network Interface Attachment.

## Import

```bash
ytofu import aws_network_interface_attachment.secondary_nic eni-attach-0a33842b4ec347c4c
```
