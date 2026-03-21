# Resource: aws_ssmincidents_replication_set

Provides a resource for managing a replication set in AWS Systems Manager Incident Manager.

## Basic Example

```yaml
resource:
  aws_ssmincidents_replication_set:
    replicationSetName:
      regions:
        name: us-west-2
      tags:
        exampleTag: exampleValue
```

## Argument Reference

This resource supports the following arguments:

* `regions` - (Optional) The replication set's Regions.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

For information about the maximum allowed number of Regions and tag value constraints, see [CreateReplicationSet in the *AWS Systems Manager Incident Manager API Reference*](https://docs.aws.amazon.com/incident-manager/latest/APIReference/API_CreateReplicationSet.html).

The `regions` configuration block supports the following arguments:

* `name` - (Required) The name of the Region, such as `ap-southeast-2`.
* `kms_key_arn` - (Optional) The Amazon Resource name (ARN) of the customer managed key. If omitted, AWS manages the AWS KMS keys for you, using an AWS owned key, as indicated by a default value of `DefaultKey`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the replication set.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `created_by` - The ARN of the user who created the replication set.
* `created_time` - A timestamp showing when the replication set was created.
* `deletion_protected` - If `true`, the last region in a replication set cannot be deleted.
* `last_modified_by` - A timestamp showing when the replication set was last modified.
* `last_modified_time` - When the replication set was last modified
* `status` - The overall status of a replication set.
    * Valid Values: `ACTIVE` | `CREATING` | `UPDATING` | `DELETING` | `FAILED`

In addition to the preceding arguments, the `regions` configuration block exports the following attributes for each Region:

* `status` - The current status of the Region.
    * Valid Values: `ACTIVE` | `CREATING` | `UPDATING` | `DELETING` | `FAILED`
* `status_update_time` - A timestamp showing when the Region status was last updated.
* `status_message` - More information about the status of a Region.

## Timeouts

Configuration options:

* `create` - (Default `120m`)
* `update` - (Default `120m`)
* `delete` - (Default `120m`)

## Import

```bash
ytofu import aws_ssmincidents_replication_set.replicationSetName import
```
