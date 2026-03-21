# Resource: aws_securityhub_configuration_policy_association

Manages Security Hub configuration policy associations.

## Basic Example

```yaml
resource:
  aws_securityhub_finding_aggregator:
    example:
      linking_mode: ALL_REGIONS

resource:
  aws_securityhub_organization_configuration:
    example:
      auto_enable: false
      auto_enable_standards: NONE
      organization_configuration:
        configuration_type: CENTRAL
      depends_on: 
        - ${aws_securityhub_finding_aggregator.example}

resource:
  aws_securityhub_configuration_policy:
    example:
      name: Example
      description: This is an example configuration policy
      configuration_policy:
        service_enabled: true
        enabled_standard_arns:
          - "arn:aws:securityhub:us-east-1::standards/aws-foundational-security-best-practices/v/1.0.0"
          - "arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0"
        security_controls_configuration:
          disabled_control_identifiers: []
      depends_on: 
        - ${aws_securityhub_organization_configuration.example}

resource:
  aws_securityhub_configuration_policy_association:
    account_example:
      target_id: 123456789012
      policy_id: ${aws_securityhub_configuration_policy.example.id}

resource:
  aws_securityhub_configuration_policy_association:
    root_example:
      target_id: r-abcd
      policy_id: ${aws_securityhub_configuration_policy.example.id}

resource:
  aws_securityhub_configuration_policy_association:
    ou_example:
      target_id: ou-abcd-12345678
      policy_id: ${aws_securityhub_configuration_policy.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `policy_id` - (Required) The universally unique identifier (UUID) of the configuration policy.
* `target_id` - (Required, Forces new resource) The identifier of the target account, organizational unit, or the root to associate with the specified configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The identifier of the target account, organizational unit, or the root that is associated with the configuration.

## Timeouts

Configuration options:

* `create` - (Default `90s`)
* `update` - (Default `90s`)

## Import

```bash
ytofu import aws_securityhub_configuration_policy_association.example_account_association 123456789012
```
