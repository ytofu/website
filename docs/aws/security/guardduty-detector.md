# Guardduty Detector

Manage Guardduty Detector resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_guardduty_detector:
    MyDetector:
      enable: true
      datasources:
        s3_logs:
          enable: true
        kubernetes:
          audit_logs:
            enable: false
        malware_protection:
          scan_ec2_instance_with_findings:
            ebs_volumes:
              enable: true
```
