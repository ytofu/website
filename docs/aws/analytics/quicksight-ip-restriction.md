# Resource: aws_quicksight_ip_restriction

Manages the content and status of IP rules.

## Basic Example

```yaml
resource:
  aws_quicksight_ip_restriction:
    example:
      enabled: true
      ip_restriction_rule_map: 
      vpc_id_restriction_rule_map: 
```

## Argument Reference

This resource supports the following arguments:

* `aws_account_id` - (Optional, Forces new resource) AWS account ID. Defaults to automatically determined account ID of the ytofu AWS provider.
* `enabled` - (Required) Whether IP rules are turned on.
* `ip_restriction_rule_map` - (Optional) Map of allowed IPv4 CIDR ranges and descriptions.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_endpoint_id_restriction_rule_map` - (Optional) Map of allowed VPC endpoint IDs and descriptions.
* `vpc_id_restriction_rule_map` - (Optional) Map of VPC IDs and descriptions. Traffic from all VPC endpoints that are present in the specified VPC is allowed.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_quicksight_ip_restriction.example "012345678901"
```
