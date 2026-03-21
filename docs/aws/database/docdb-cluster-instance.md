# Docdb Cluster Instance

Manage Docdb Cluster Instance resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_docdb_cluster_instance:
    cluster_instances:
      identifier: "docdb-cluster-demo-${count.index}"
      cluster_identifier: ${aws_docdb_cluster.default.id}
      instance_class: db.r5.large

resource:
  aws_docdb_cluster:
    default:
      cluster_identifier: docdb-cluster-demo
      availability_zones: 
        - us-west-2a
        - us-west-2b
        - us-west-2c
      master_username: foo
      master_password: barbut8chars
```
