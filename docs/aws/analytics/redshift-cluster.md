# Redshift Cluster

Manage Redshift Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_redshift_cluster:
    example:
      cluster_identifier: tf-redshift-cluster
      database_name: mydb
      master_username: exampleuser
      master_password: Mustbe8characters
      node_type: dc1.large
      cluster_type: single-node
```

## With Managed Credentials

```yaml
resource:
  aws_redshift_cluster:
    example:
      cluster_identifier: tf-redshift-cluster
      database_name: mydb
      master_username: exampleuser
      node_type: dc1.large
      cluster_type: single-node
      manage_master_password: true
```
