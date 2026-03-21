# Networkmanager Site To Site VPN Attachment

Manage Networkmanager Site To Site VPN Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkmanager_site_to_site_vpn_attachment:
    example:
      core_network_id: ${awscc_networkmanager_core_network.example.id}
      vpn_connection_arn: ${aws_vpn_connection.example.arn}
```

## Full Usage

```yaml
resource:
  aws_customer_gateway:
    test:
      bgp_asn: 65000
      ip_address: 172.0.0.1
      type: ipsec.1

resource:
  aws_vpn_connection:
    test:
      customer_gateway_id: ${aws_customer_gateway.test.id}
      type: ipsec.1
      tags:
        Name: test

resource:
  aws_networkmanager_global_network:
    test:
      tags:
        Name: test

resource:
  awscc_networkmanager_core_network:
    test:
      global_network_id: ${aws_networkmanager_global_network.test.id}
      policy_document: example-value

data:
  aws_networkmanager_core_network_policy_document:
    test:
      core_network_configuration:
        vpn_ecmp_support: false
        asn_ranges: 
          - 64512-64555
        edge_locations:
          location: ${data.aws_region.current.region}
          asn: 64512
      segments:
        name: shared
        description: SegmentForSharedServices
        require_attachment_acceptance: true
      segment_actions:
        action: share
        mode: attachment-route
        segment: shared
        share_with: 
          - "*"
      attachment_policies:
        rule_number: 1
        condition_logic: or
        conditions:
          type: tag-value
          operator: equals
          key: segment
          value: shared
        action:
          association_method: constant
          segment: shared

resource:
  aws_networkmanager_site_to_site_vpn_attachment:
    test:
      core_network_id: ${awscc_networkmanager_core_network.test.id}
      vpn_connection_arn: ${aws_vpn_connection.test.arn}
      tags:
        segment: shared

resource:
  aws_networkmanager_attachment_accepter:
    test:
      attachment_id: ${aws_networkmanager_site_to_site_vpn_attachment.test.id}
      attachment_type: ${aws_networkmanager_site_to_site_vpn_attachment.test.attachment_type}
```
