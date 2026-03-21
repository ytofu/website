# Appflow Connector Profile

Manage Appflow Connector Profile resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy:
    example:
      name: AmazonRedshiftAllCommandsFullAccess

resource:
  aws_iam_role:
    example:
      name: example_role
      managed_policy_arns: 
        - ${data.aws_iam_policy.test.arn}
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "ec2.amazonaws.com" } }, ] }'

resource:
  aws_s3_bucket:
    example:
      bucket: example-bucket

resource:
  aws_redshift_cluster:
    example:
      cluster_identifier: example_cluster
      database_name: example_db
      master_username: exampleuser
      master_password: examplePassword123!
      node_type: dc1.large
      cluster_type: single-node

resource:
  aws_appflow_connector_profile:
    example:
      name: example_profile
      connector_type: Redshift
      connection_mode: Public
      connector_profile_config:
        connector_profile_credentials:
          redshift:
            password: ${aws_redshift_cluster.example.master_password}
            username: ${aws_redshift_cluster.example.master_username}
        connector_profile_properties:
          redshift:
            bucket_name: ${aws_s3_bucket.example.name}
            database_url: "jdbc:redshift://${aws_redshift_cluster.example.endpoint}/${aws_redshift_cluster.example.database_name}"
            role_arn: ${aws_iam_role.example.arn}
```
