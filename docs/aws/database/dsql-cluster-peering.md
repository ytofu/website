# Resource: aws_dsql_cluster_peering

ytofu resource for managing an Amazon Aurora DSQL Cluster Peering.

## Basic Example

```yaml
resource:
  aws_dsql_cluster:
    example_1:
      multi_region_properties:
        witness_region: us-west-2

  aws_dsql_cluster:
    example_2:
      multi_region_properties:
        witness_region: us-west-2

  aws_dsql_cluster_peering:
    example_1:
      identifier: ${aws_dsql_cluster.example_1.identifier}
      clusters: 
        - ${aws_dsql_cluster.example_2.arn}
      witness_region: ${aws_dsql_cluster.example_1.multi_region_properties[0].witness_region}

  aws_dsql_cluster_peering:
    example_2:
      identifier: ${aws_dsql_cluster.example_2.identifier}
      clusters: 
        - ${aws_dsql_cluster.example_1.arn}
      witness_region: ${aws_dsql_cluster.example_2.multi_region_properties[0].witness_region}```

## Argument Reference

This resource supports the following arguments:

* `clusters` - (Required) List of DSQL Cluster ARNs to be peered to this cluster.
* `identifier` - (Required) DSQL Cluster Identifier.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `witness_region` - (Required) Witness region for a multi-region cluster.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `30m`)

## Import

```bash
ytofu import aws_dsql_cluster_peering.example cluster-id-12345678
```
