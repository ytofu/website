# Securityhub Configuration Policy

Manage Securityhub Configuration Policy resources using ytofu YAML.

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
```

## Disabled Policy

```yaml
resource:
  aws_securityhub_configuration_policy:
    disabled:
      name: Disabled
      description: This is an example of disabled configuration policy
      configuration_policy:
        service_enabled: false
      depends_on: 
        - ${aws_securityhub_organization_configuration.example}
```

## Custom Control Configuration

```yaml
resource:
  aws_securityhub_configuration_policy:
    disabled:
      name: Custom Controls
      description: This is an example of configuration policy with custom control settings
      configuration_policy:
        service_enabled: true
        enabled_standard_arns:
          - "arn:aws:securityhub:us-east-1::standards/aws-foundational-security-best-practices/v/1.0.0"
          - "arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0"
        security_controls_configuration:
          enabled_control_identifiers:
            - APIGateway.1
            - IAM.7
          security_control_custom_parameter:
            security_control_id: APIGateway.1
            parameter:
              name: loggingLevel
              value_type: CUSTOM
              enum:
                value: INFO
          security_control_custom_parameter:
            security_control_id: IAM.7
            parameter:
              name: RequireLowercaseCharacters
              value_type: CUSTOM
              bool:
                value: false
            parameter:
              name: MaxPasswordAge
              value_type: CUSTOM
              int:
                value: 60
      depends_on: 
        - ${aws_securityhub_organization_configuration.example}
```
