# Mwaa Environment

Manage Mwaa Environment resources using ytofu YAML.

## Basic Usage

```yaml
resource:
  aws_mwaa_environment:
    example:
      dag_s3_path: dags/
      execution_role_arn: ${aws_iam_role.example.arn}
      name: example
      network_configuration:
        security_group_ids: 
          - ${aws_security_group.example.id}
        subnet_ids: ${aws_subnet.private[*].id}
      source_bucket_arn: ${aws_s3_bucket.example.arn}
```

## Example with Airflow configuration options

```yaml
resource:
  aws_mwaa_environment:
    example:
      airflow_configuration_options: 
      dag_s3_path: dags/
      execution_role_arn: ${aws_iam_role.example.arn}
      name: example
      network_configuration:
        security_group_ids: 
          - ${aws_security_group.example.id}
        subnet_ids: ${aws_subnet.private[*].id}
      source_bucket_arn: ${aws_s3_bucket.example.arn}
```

## Example with logging configurations

```yaml
resource:
  aws_mwaa_environment:
    example:
      dag_s3_path: dags/
      execution_role_arn: ${aws_iam_role.example.arn}
      logging_configuration:
        dag_processing_logs:
          enabled: true
          log_level: DEBUG
        scheduler_logs:
          enabled: true
          log_level: INFO
        task_logs:
          enabled: true
          log_level: WARNING
        webserver_logs:
          enabled: true
          log_level: ERROR
        worker_logs:
          enabled: true
          log_level: CRITICAL
      name: example
      network_configuration:
        security_group_ids: 
          - ${aws_security_group.example.id}
        subnet_ids: ${aws_subnet.private[*].id}
      source_bucket_arn: ${aws_s3_bucket.example.arn}
```

## Example with tags

```yaml
resource:
  aws_mwaa_environment:
    example:
      dag_s3_path: dags/
      execution_role_arn: ${aws_iam_role.example.arn}
      name: example
      network_configuration:
        security_group_ids: 
          - ${aws_security_group.example.id}
        subnet_ids: ${aws_subnet.private[*].id}
      source_bucket_arn: ${aws_s3_bucket.example.arn}
      tags:
        Name: example
        Environment: production
```
