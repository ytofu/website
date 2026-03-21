# Route53 Traffic Policy

Manage Route53 Traffic Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_route53_traffic_policy:
    example:
      name: example
      comment: example comment
      document: |
        {
        "AWSPolicyFormatVersion": "2015-10-01",
        "RecordType": "A",
        "Endpoints": {
        "endpoint-start-NkPh": {
        "Type": "value",
        "Value": "10.0.0.2"
        }
        },
        "StartEndpoint": "endpoint-start-NkPh"
        }
```
