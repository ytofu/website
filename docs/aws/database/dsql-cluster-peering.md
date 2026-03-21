# Dsql Cluster Peering

Manage Dsql Cluster Peering resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dsql_cluster:
    example_1:
      multi_region_properties:
        witness_region: us-west-2

resource:
  aws_dsql_cluster:
    example_2:
      multi_region_properties:
        witness_region: us-west-2

resource:
  aws_dsql_cluster_peering:
    example_1:
      identifier: ${aws_dsql_cluster.example_1.identifier}
      clusters: 
        - ${aws_dsql_cluster.example_2.arn}
      witness_region: ${aws_dsql_cluster.example_1.multi_region_properties[0].witness_region}

resource:
  aws_dsql_cluster_peering:
    example_2:
      identifier: ${aws_dsql_cluster.example_2.identifier}
      clusters: 
        - ${aws_dsql_cluster.example_1.arn}
      witness_region: ${aws_dsql_cluster.example_2.multi_region_properties[0].witness_region}
```
