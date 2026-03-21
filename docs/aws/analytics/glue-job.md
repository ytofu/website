# Glue Job

Manage Glue Job resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_job:
    etl_job:
      name: example-etl-job
      description: An example Glue ETL job
      role_arn: ${aws_iam_role.glue_job_role.arn}
      glue_version: 5.0
      max_retries: 0
      timeout: 2880
      number_of_workers: 2
      worker_type: G.1X
      connections: 
        - ${aws_glue_connection.example.name}
      execution_class: STANDARD
      command:
        script_location: "s3://${aws_s3_bucket.glue_scripts.bucket}/jobs/etl_job.py"
        name: glueetl
        python_version: 3
      notification_property:
        notify_delay_after: 3
      default_arguments: 
      execution_property:
        max_concurrent_runs: 1
      tags: 

resource:
  aws_iam_role:
    glue_job_role:
      name: glue-job-role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "glue.amazonaws.com" } } ] }'

resource:
  aws_s3_object:
    glue_etl_script:
      bucket: ${aws_s3_bucket.glue_scripts.id}
      key: jobs/etl_job.py
      source: "jobs/etl_job.py" # Make sure this file exists locally
```

## Pythonshell Job

```yaml
resource:
  aws_glue_job:
    python_shell_job:
      name: example-python-shell-job
      description: An example Python shell job
      role_arn: ${aws_iam_role.glue_job_role.arn}
      max_capacity: 0.0625
      max_retries: 0
      timeout: 2880
      connections: 
        - ${aws_glue_connection.example.name}
      command:
        script_location: "s3://${aws_s3_bucket.glue_scripts.bucket}/jobs/shell_job.py"
        name: pythonshell
        python_version: 3.9
      default_arguments: 
      execution_property:
        max_concurrent_runs: 1
      tags: 

resource:
  aws_iam_role:
    glue_job_role:
      name: glue-job-role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "glue.amazonaws.com" } } ] }'

resource:
  aws_s3_object:
    python_shell_script:
      bucket: ${aws_s3_bucket.glue_scripts.id}
      key: jobs/shell_job.py
      source: "jobs/shell_job.py" # Make sure this file exists locally
```

## Ray Job

```yaml
resource:
  aws_glue_job:
    example:
      name: example
      role_arn: ${aws_iam_role.example.arn}
      glue_version: 4.0
      worker_type: Z.2X
      command:
        name: glueray
        python_version: 3.9
        runtime: Ray2.4
        script_location: "s3://${aws_s3_bucket.example.bucket}/example.py"
```

## Scala Job

```yaml
resource:
  aws_glue_job:
    example:
      name: example
      role_arn: ${aws_iam_role.example.arn}
      command:
        script_location: "s3://${aws_s3_bucket.example.bucket}/example.scala"
      default_arguments: 
```

## Streaming Job

```yaml
resource:
  aws_glue_job:
    example:
      name: example streaming job
      role_arn: ${aws_iam_role.example.arn}
      command:
        name: gluestreaming
        script_location: "s3://${aws_s3_bucket.example.bucket}/example.script"
```

## Enabling CloudWatch Logs and Metrics

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: example
      retention_in_days: 14

resource:
  aws_glue_job:
    example:
      default_arguments: 
```
