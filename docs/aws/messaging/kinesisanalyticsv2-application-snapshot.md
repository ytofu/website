# Resource: aws_kinesisanalyticsv2_application_snapshot

Manages a Kinesis Analytics v2 Application Snapshot.
Snapshots are the AWS implementation of [Flink Savepoints](https://ci.apache.org/projects/flink/flink-docs-release-1.11/ops/state/savepoints.html).

## Basic Example

```yaml
resource:
  aws_kinesisanalyticsv2_application_snapshot:
    example:
      application_name: ${aws_kinesisanalyticsv2_application.example.name}
      snapshot_name: example-snapshot
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `application_name` - (Required) The name of an existing  Kinesis Analytics v2 Application. Note that the application must be running for a snapshot to be created.
* `snapshot_name` - (Required) The name of the application snapshot.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The application snapshot identifier.
* `application_version_id` - The current application version ID when the snapshot was created.
* `snapshot_creation_timestamp` - The timestamp of the application snapshot.

## Timeouts

Configuration options:

- `create` - (Default `10m`)
- `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_kinesisanalyticsv2_application_snapshot.example example-application/example-snapshot
```
