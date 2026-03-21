# Resource: aws_dsql_cluster

ytofu resource for managing an Amazon Aurora DSQL Cluster.

## Basic Example

```yaml
resource:
  aws_dsql_cluster:
    example:
      deletion_protection_enabled: true
      tags:
        Name: TestCluster
```

## Argument Reference

This resource supports the following arguments:

* `deletion_protection_enabled` - (Optional) Whether deletion protection is enabled in this cluster.
  Default value is `false`.
* `force_destroy` - (Optional) Destroys cluster even if `deletion_protection_enabled` is set to `true`.
  Default value is `false`.
* `kms_encryption_key` - (Optional) The ARN of the AWS KMS key that encrypts data in the DSQL Cluster, or `"AWS_OWNED_KMS_KEY"`.
* `multi_region_properties` - (Optional) Multi-region properties of the DSQL Cluster.
    * `witness_region` - (Required) Witness region for the multi-region clusters. Setting this makes this cluster a multi-region cluster. Changing it recreates the resource.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `tags` - (Optional) Set of tags to be associated with the AWS DSQL Cluster resource.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Cluster.
* `encryption_details` - Encryption configuration details for the DSQL Cluster.
    * `encryption_status` - The status of encryption for the DSQL Cluster.
    * `encryption_type` - The type of encryption that protects the data on the DSQL Cluster.
* `identifier` - Cluster Identifier.
* `multi_region_properties` - Multi-region properties of the DSQL Cluster.
    * `clusters` - List of DSQL Cluster ARNs peered to this cluster.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `vpc_endpoint_service_name` - The DSQL Cluster's VPC endpoint service name.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_dsql_cluster.example abcde1f234ghijklmnop5qr6st
```
