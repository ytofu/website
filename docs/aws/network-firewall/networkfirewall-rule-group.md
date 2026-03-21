# Networkfirewall Rule Group

Manage Networkfirewall Rule Group resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_networkfirewall_rule_group:
    example:
      capacity: 100
      name: example
      type: STATEFUL
      rule_group:
        rules_source:
          rules_source_list:
            generated_rules_type: DENYLIST
            target_types: 
              - HTTP_HOST
            targets: 
              - test.example.com
      tags:
        Tag1: Value1
        Tag2: Value2
```

## Stateful Inspection for permitting packets from a source IP address

```yaml
resource:
  aws_networkfirewall_rule_group:
    example:
      capacity: 50
      description: Permits http traffic from source
      name: example
      type: STATEFUL
      rule_group:
        rules_source:
      tags:
        Name: permit HTTP from source
```

## Stateful Inspection for blocking packets from going to an intended destination

```yaml
resource:
  aws_networkfirewall_rule_group:
    example:
      capacity: 100
      name: example
      type: STATEFUL
      rule_group:
        rules_source:
          stateful_rule:
            action: DROP
            header:
              destination: 124.1.1.24/32
              destination_port: 53
              direction: ANY
              protocol: TCP
              source: 1.2.3.4/32
              source_port: 53
            rule_option:
              keyword: sid
              settings: 
                - 1
      tags:
        Tag1: Value1
        Tag2: Value2
```

## Stateful Inspection from rules specifications defined in Suricata flat format

```yaml
resource:
  aws_networkfirewall_rule_group:
    example:
      capacity: 100
      name: example
      type: STATEFUL
      rules: file-content
      tags:
        Tag1: Value1
        Tag2: Value2
```

## Stateful Inspection from rule group specifications using rule variables and Suricata format rules

```yaml
resource:
  aws_networkfirewall_rule_group:
    example:
      capacity: 100
      name: example
      type: STATEFUL
      rule_group:
        rule_variables:
          ip_sets:
            key: WEBSERVERS_HOSTS
            ip_set:
              definition: 
                - 10.0.0.0/16
                - 10.0.1.0/24
                - 192.168.0.0/16
          ip_sets:
            key: EXTERNAL_HOST
            ip_set:
              definition: 
                - 1.2.3.4/32
          port_sets:
            key: HTTP_PORTS
            port_set:
              definition: 
                - 443
                - 80
        rules_source:
          rules_string: file-content
      tags:
        Tag1: Value1
        Tag2: Value2
```

## Stateless Inspection with a Custom Action

```yaml
resource:
  aws_networkfirewall_rule_group:
    example:
      description: Stateless Rate Limiting Rule
      capacity: 100
      name: example
      type: STATELESS
      rule_group:
        rules_source:
          stateless_rules_and_custom_actions:
            custom_action:
              action_definition:
                publish_metric_action:
                  dimension:
                    value: 2
              action_name: ExampleMetricsAction
            stateless_rule:
              priority: 1
              rule_definition:
                actions: 
                  - "aws:pass"
                  - ExampleMetricsAction
                match_attributes:
                  source:
                    address_definition: 1.2.3.4/32
                  source_port:
                    from_port: 443
                    to_port: 443
                  destination:
                    address_definition: 124.1.1.5/32
                  destination_port:
                    from_port: 443
                    to_port: 443
                  protocols: 
                    - 6
                  tcp_flag:
                    flags: 
                      - SYN
                    masks: 
                      - SYN
                      - ACK
      tags:
        Tag1: Value1
        Tag2: Value2
```

## IP Set References to the Rule Group

```yaml
resource:
  aws_networkfirewall_rule_group:
    example:
      capacity: 100
      name: example
      type: STATEFUL
      rule_group:
        rules_source:
          rules_source_list:
            generated_rules_type: DENYLIST
            target_types: 
              - HTTP_HOST
            targets: 
              - test.example.com
        reference_sets:
          ip_set_references:
            key: example
            ip_set_reference:
              reference_arn: ${aws_ec2_managed_prefix_list.this.arn}
      tags:
        Tag1: Value1
        Tag2: Value2
```

## Example with S3 as source for the suricata rules

```yaml
data:
  aws_s3_object:
    suricata_rules:
      bucket: ${aws_s3_bucket.suricata_rules.id}
      key: rules/custom.rules

resource:
  aws_networkfirewall_rule_group:
    s3_rules_example:
      capacity: 1000
      name: my-terraform-s3-rules
      type: STATEFUL
      rule_group:
        rule_variables:
          ip_sets:
            key: HOME_NET
            ip_set:
              definition: 
                - 10.0.0.0/16
                - 192.168.0.0/16
                - 172.16.0.0/12
          port_sets:
            key: HTTP_PORTS
            port_set:
              definition: 
                - 443
                - 80
        rules_source:
          rules_string: ${data.aws_s3_object.suricata_rules.body}
      tags:
        ManagedBy: terraform
```
