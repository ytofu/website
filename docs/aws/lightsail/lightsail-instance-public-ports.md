# Resource: aws_lightsail_instance_public_ports

Manages public ports for a Lightsail instance. Use this resource to open ports for a specific Amazon Lightsail instance and specify the IP addresses allowed to connect to the instance through the ports and the protocol.

## Basic Example

```yaml
data:
  aws_availability_zones:
    available:
      state: available
      filter:
        name: opt-in-status
        values: 
          - opt-in-not-required

resource:
  aws_lightsail_instance:
    example:
      name: example-instance
      availability_zone: ${data.aws_availability_zones.available.names[0]}
      blueprint_id: amazon_linux_2
      bundle_id: nano_3_0

  aws_lightsail_instance_public_ports:
    example:
      instance_name: ${aws_lightsail_instance.example.name}
      port_info:
        protocol: tcp
        from_port: 80
        to_port: 80
      port_info:
        protocol: tcp
        from_port: 443
        to_port: 443
        cidrs: 
          - 192.168.1.0/24```

## Argument Reference

The following arguments are required:

* `instance_name` - (Required) Name of the instance for which to open ports.
* `port_info` - (Required) Descriptor of the ports to open for the specified instance. AWS closes all currently open ports that are not included in this argument. See [`port_info` Block](#port_info-block) for details.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

### `port_info` Block

The `port_info` configuration block supports the following arguments:

* `from_port` - (Required) First port in a range of open ports on an instance. See [PortInfo](https://docs.aws.amazon.com/lightsail/2016-11-28/api-reference/API_PortInfo.html) for details.
* `protocol` - (Required) IP protocol name. Valid values: `tcp`, `all`, `udp`, `icmp`, `icmpv6`. See [PortInfo](https://docs.aws.amazon.com/lightsail/2016-11-28/api-reference/API_PortInfo.html) for details.
* `to_port` - (Required) Last port in a range of open ports on an instance. See [PortInfo](https://docs.aws.amazon.com/lightsail/2016-11-28/api-reference/API_PortInfo.html) for details.
* `cidr_list_aliases` - (Optional) Set of CIDR aliases that define access for a preconfigured range of IP addresses.
* `cidrs` - (Optional) Set of IPv4 addresses or ranges of IPv4 addresses (in CIDR notation) that are allowed to connect to an instance through the ports, and the protocol.
* `ipv6_cidrs` - (Optional) Set of IPv6 addresses or ranges of IPv6 addresses (in CIDR notation) that are allowed to connect to an instance through the ports, and the protocol.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the resource.
