# Resource: aws_security_group

Provides a security group resource.

## Basic Example

```yaml
resource:
  aws_security_group:
    allow_tls:
      name: allow_tls
      description: Allow TLS inbound traffic and all outbound traffic
      vpc_id: ${aws_vpc.main.id}
      tags:
        Name: allow_tls

  aws_vpc_security_group_ingress_rule:
    allow_tls_ipv4:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv4: ${aws_vpc.main.cidr_block}
      from_port: 443
      ip_protocol: tcp
      to_port: 443

  aws_vpc_security_group_ingress_rule:
    allow_tls_ipv6:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv6: ${aws_vpc.main.ipv6_cidr_block}
      from_port: 443
      ip_protocol: tcp
      to_port: 443

  aws_vpc_security_group_egress_rule:
    allow_all_traffic_ipv4:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv4: 0.0.0.0/0
      ip_protocol: "-1" # semantically equivalent to all ports

  aws_vpc_security_group_egress_rule:
    allow_all_traffic_ipv6:
      security_group_id: ${aws_security_group.allow_tls.id}
      cidr_ipv6: "::/0"
      ip_protocol: "-1" # semantically equivalent to all ports```

## Usage With Prefix List IDs

```yaml
resource:
  aws_security_group:
    example:
      egress:
        from_port: 0
        to_port: 0
        protocol: -1
        prefix_list_ids: 
          - ${aws_vpc_endpoint.my_endpoint.prefix_list_id}

  aws_vpc_endpoint:
    my_endpoint:```

## Removing All Ingress and Egress Rules

```yaml
resource:
  aws_security_group:
    example:
      name: sg
      vpc_id: ${aws_vpc.example.id}
      ingress: []
      egress: []
```

## Recreating a Security Group

```yaml
resource:
  aws_security_group:
    example:
      name: changeable-name
      lifecycle:
        create_before_destroy: true
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional, Forces new resource) Security group description. Defaults to `Managed by ytofu`. Cannot be `""`. **NOTE**: This field maps to the AWS `GroupDescription` attribute, for which there is no Update API. If you'd like to classify your security groups in a way that can be updated, use `tags`.
* `egress` - (Optional, VPC only) Configuration block for egress rules. Can be specified multiple times for each egress rule. Each egress block supports fields documented below. This argument is processed in attribute-as-blocks mode.
* `ingress` - (Optional) Configuration block for ingress rules. Can be specified multiple times for each ingress rule. Each ingress block supports fields documented below. This argument is processed in attribute-as-blocks mode.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `name` - (Optional, Forces new resource) Name of the security group. If omitted, ytofu will assign a random, unique name.
* `revoke_rules_on_delete` - (Optional) Instruct ytofu to revoke all of the Security Groups attached ingress and egress rules before deleting the rule itself. This is normally not needed, however certain AWS services such as Elastic Map Reduce may automatically add required rules to security groups used with the service, and those rules may contain a cyclic dependency that prevent the security groups from being destroyed without removing the dependency first. Default `false`.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `vpc_id` - (Optional, Forces new resource) VPC ID. Defaults to the region's default VPC.

### ingress

This argument is processed in attribute-as-blocks mode.

The following arguments are required:

* `from_port` - (Required) Start port (or ICMP type number if protocol is `icmp` or `icmpv6`).
* `to_port` - (Required) End range port (or ICMP code if protocol is `icmp`).
* `protocol` - (Required) Protocol. If you select a protocol of `-1` (semantically equivalent to `all`, which is not a valid value here), you must specify a `from_port` and `to_port` equal to 0. The supported values are defined in the `IpProtocol` argument on the [IpPermission](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_IpPermission.html) API reference. This argument is normalized to a lowercase value to match the AWS API requirement when using with ytofu 0.12.x and above, please make sure that the value of the protocol is specified as lowercase when using with older version of ytofu to avoid an issue during upgrade.

The following arguments are optional:

* `cidr_blocks` - (Optional) List of CIDR blocks.
* `description` - (Optional) Description of this ingress rule.
* `ipv6_cidr_blocks` - (Optional) List of IPv6 CIDR blocks.
* `prefix_list_ids` - (Optional) List of Prefix List IDs.
* `security_groups` - (Optional) List of security groups. A group name can be used relative to the default VPC. Otherwise, group ID.
* `self` - (Optional) Whether the security group itself will be added as a source to this ingress rule.

### egress

This argument is processed in attribute-as-blocks mode.

The following arguments are required:

* `from_port` - (Required) Start port (or ICMP type number if protocol is `icmp`)
* `to_port` - (Required) End range port (or ICMP code if protocol is `icmp`).

The following arguments are optional:

* `cidr_blocks` - (Optional) List of CIDR blocks.
* `description` - (Optional) Description of this egress rule.
* `ipv6_cidr_blocks` - (Optional) List of IPv6 CIDR blocks.
* `prefix_list_ids` - (Optional) List of Prefix List IDs.
* `protocol` - (Required) Protocol. If you select a protocol of `-1` (semantically equivalent to `all`, which is not a valid value here), you must specify a `from_port` and `to_port` equal to 0. The supported values are defined in the `IpProtocol` argument in the [IpPermission](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_IpPermission.html) API reference. This argument is normalized to a lowercase value to match the AWS API requirement when using ytofu 0.12.x and above. Please make sure that the value of the protocol is specified as lowercase when used with older version of ytofu to avoid issues during upgrade.
* `security_groups` - (Optional) List of security groups. A group name can be used relative to the default VPC. Otherwise, group ID.
* `self` - (Optional) Whether the security group itself will be added as a source to this egress rule.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the security group.
* `id` - ID of the security group.
* `owner_id` - Owner ID.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `delete` - (Default `15m`)

## Import

```bash
ytofu import aws_security_group.example sg-903004f8
```
