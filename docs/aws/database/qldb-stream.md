# Qldb Stream

Manage Qldb Stream resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_qldb_stream:
    example:
      ledger_name: existing-ledger-name
      stream_name: sample-ledger-stream
      role_arn: sample-role-arn
      inclusive_start_time: "2021-01-01T00:00:00Z"
      kinesis_configuration:
        aggregation_enabled: false
        stream_arn: "arn:aws:kinesis:us-east-1:xxxxxxxxxxxx:stream/example-kinesis-stream"
      tags: 
```
