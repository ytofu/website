# Default Network Acl

Manage Default Network Acl resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc:
    mainvpc:
      cidr_block: 10.1.0.0/16

resource:
  aws_default_network_acl:
    default:
      default_network_acl_id: ${aws_vpc.mainvpc.default_network_acl_id}
      ingress:
        protocol: -1
        rule_no: 100
        action: allow
        cidr_block: 0.0.0.0/0
        from_port: 0
        to_port: 0
      egress:
        protocol: -1
        rule_no: 100
        action: allow
        cidr_block: 0.0.0.0/0
        from_port: 0
        to_port: 0
```

## Example: Deny All Egress Traffic, Allow Ingress

```yaml
resource:
  aws_vpc:
    mainvpc:
      cidr_block: 10.1.0.0/16

resource:
  aws_default_network_acl:
    default:
      default_network_acl_id: ${aws_vpc.mainvpc.default_network_acl_id}
      ingress:
        protocol: -1
        rule_no: 100
        action: allow
        cidr_block: ${aws_default_vpc.mainvpc.cidr_block}
        from_port: 0
        to_port: 0
```

## Example: Deny All Traffic To Any Subnet In The Default Network ACL

```yaml
resource:
  aws_vpc:
    mainvpc:
      cidr_block: 10.1.0.0/16

resource:
  aws_default_network_acl:
    default:
      default_network_acl_id: ${aws_vpc.mainvpc.default_network_acl_id}
```

## Managing Subnets In A Default Network ACL

```yaml
resource:
  aws_default_network_acl:
    default:
      lifecycle:
        ignore_changes: 
          - subnet_ids
```
