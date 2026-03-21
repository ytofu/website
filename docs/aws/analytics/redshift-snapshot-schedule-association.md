# Resource: aws_redshift_snapshot_schedule_association

## Example Usage

## Basic Example

```yaml
resource:
  aws_redshift_cluster:
    default:
      cluster_identifier: tf-redshift-cluster
      database_name: mydb
      master_username: foo
      master_password: Mustbe8characters
      node_type: dc1.large
      cluster_type: single-node

resource:
  aws_redshift_snapshot_schedule:
    default:
      identifier: tf-redshift-snapshot-schedule
      definitions:
        - rate(12 hours)

resource:
  aws_redshift_snapshot_schedule_association:
    default:
      cluster_identifier: ${aws_redshift_cluster.default.id}
      schedule_identifier: ${aws_redshift_snapshot_schedule.default.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cluster_identifier` - (Required, Forces new resource) The cluster identifier.
* `schedule_identifier` - (Required, Forces new resource) The snapshot schedule identifier.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_redshift_snapshot_schedule_association.default tf-redshift-cluster/tf-redshift-snapshot-schedule
```
