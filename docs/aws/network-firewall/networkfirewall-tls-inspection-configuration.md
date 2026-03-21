# Networkfirewall TLS Inspection Configuration

Manage Networkfirewall TLS Inspection Configuration resources using ytofu YAML.

## Combined inbound and outbound

```yaml
resource:
  aws_networkfirewall_tls_inspection_configuration:
    example:
      name: example
      description: example
      encryption_configuration:
        key_id: AWS_OWNED_KMS_KEY
        type: AWS_OWNED_KMS_KEY
      tls_inspection_configuration:
        server_certificate_configuration:
          certificate_authority_arn: ${aws_acm_certificate.example_1.arn}
          check_certificate_revocation_status:
            revoked_status_action: REJECT
            unknown_status_action: PASS
          server_certificate:
            resource_arn: ${aws_acm_certificate.example_2.arn}
          scope:
            protocols: 
              - 6
            destination_ports:
              from_port: 443
              to_port: 443
            destination:
              address_definition: 0.0.0.0/0
            source_ports:
              from_port: 0
              to_port: 65535
            source:
              address_definition: 0.0.0.0/0
```
