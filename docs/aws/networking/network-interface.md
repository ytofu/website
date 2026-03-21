# Resource: aws_network_interface

Provides an Elastic network interface (ENI) resource.

## Basic Example

```yaml
resource:
  aws_network_interface:
    test:
      subnet_id: ${aws_subnet.public_a.id}
      private_ips: 
        - 10.0.0.50
      security_groups: 
        - ${aws_security_group.web.id}
      attachment:
        instance: ${aws_instance.test.id}
        device_index: 1
```

## Argument Reference

The following arguments are required:

* `subnet_id` - (Required) Subnet ID to create the ENI in.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `attachment` - (Optional) Configuration block to define the attachment of the ENI. See [Attachment](#attachment) below for more details!
* `description` - (Optional) Description for the network interface.
* `enable_primary_ipv6` - (Optional) Enables assigning a primary IPv6 Global Unicast Address (GUA) to the network interface (ENI) in dual-stack or IPv6-only subnets. This ensures the instance attached to the ENI retains a consistent IPv6 address. Once enabled, the first IPv6 GUA becomes the primary IPv6 address and cannot be disabled. The primary IPv6 address remains assigned until the instance is terminated or the ENI is detached. Enabling and subsequent disabling forces recreation of the ENI.
* `interface_type` - (Optional) Type of network interface to create. Set to `efa` for Elastic Fabric Adapter. Changing `interface_type` will cause the resource to be destroyed and re-created.
* `ipv4_prefix_count` - (Optional) Number of IPv4 prefixes that AWS automatically assigns to the network interface.
* `ipv4_prefixes` - (Optional) One or more IPv4 prefixes assigned to the network interface.
* `ipv6_address_count` - (Optional) Number of IPv6 addresses to assign to a network interface. You can't use this option if specifying specific `ipv6_addresses`. If your subnet has the AssignIpv6AddressOnCreation attribute set to `true`, you can specify `0` to override this setting.
* `ipv6_address_list_enabled` - (Optional) Whether `ipv6_address_list` is allowed and controls the IPs to assign to the ENI and `ipv6_addresses` and `ipv6_address_count` become read-only. Default is `false`.
* `ipv6_address_list` - (Optional) List of private IPs to assign to the ENI in sequential order.
* `ipv6_addresses` - (Optional) One or more specific IPv6 addresses from the IPv6 CIDR block range of your subnet. Addresses are assigned without regard to order. You can't use this option if you're specifying `ipv6_address_count`.
* `ipv6_prefix_count` - (Optional) Number of IPv6 prefixes that AWS automatically assigns to the network interface.
* `ipv6_prefixes` - (Optional) One or more IPv6 prefixes assigned to the network interface.
* `private_ip_list` - (Optional) List of private IPs to assign to the ENI in sequential order. Requires setting `private_ip_list_enabled` to `true`.
* `private_ip_list_enabled` - (Optional) Whether `private_ip_list` is allowed and controls the IPs to assign to the ENI and `private_ips` and `private_ips_count` become read-only. Default is `false`.
* `private_ips` - (Optional) List of private IPs to assign to the ENI without regard to order.
* `private_ips_count` - (Optional) Number of secondary private IPs to assign to the ENI. The total number of private IPs will be 1 + `private_ips_count`, as a primary private IP will be assiged to an ENI by default.
* `security_groups` - (Optional) List of security group IDs to assign to the ENI.
* `source_dest_check` - (Optional) Whether to enable source destination checking for the ENI. Default true.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### Attachment

The `attachment` block supports the following:

* `instance` - (Required) ID of the instance to attach to.
* `device_index` - (Required) Integer to define the devices index.
* `network_card_index` - (Optional) Index of the network card. Specify a value greater than 0 when using multiple network cards, which are supported by [some instance types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html#network-cards). The default is 0.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the network interface.
* `id` - ID of the network interface.
* `mac_address` - MAC address of the network interface.
* `owner_id` - AWS account ID of the owner of the network interface.
* `private_dns_name` - Private DNS name of the network interface (IPv4).
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_network_interface.test eni-e5aa89a3
```
