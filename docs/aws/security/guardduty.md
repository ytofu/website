# GuardDuty

Enable and configure Amazon GuardDuty threat detection using ytofu YAML.

## Enable GuardDuty

```yaml
resource:
  aws_guardduty_detector:
    example:
      enable: true
```

## With Data Sources

```yaml
resource:
  aws_guardduty_detector:
    example:
      enable: true
      datasources:
        s3_logs:
          enable: true
        kubernetes:
          audit_logs:
            enable: true
        malware_protection:
          scan_ec2_instance_with_findings:
            ebs_volumes:
              enable: true
```

## GuardDuty Filter

```yaml
resource:
  aws_guardduty_filter:
    example:
      name: example
      action: ARCHIVE
      detector_id: ${aws_guardduty_detector.example.id}
      rank: 1
      finding_criteria:
        criterion:
          - field: type
            equals:
              - Recon:EC2/PortProbeUnprotectedPort
          - field: updatedAt
            greater_than_or_equal: "2023-01-01T00:00:00Z"
```
