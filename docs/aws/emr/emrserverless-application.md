# Emrserverless Application

Manage Emrserverless Application resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_emrserverless_application:
    example:
      name: example
      release_label: emr-6.6.0
      type: hive
```

## Initial Capacity Usage

```yaml
resource:
  aws_emrserverless_application:
    example:
      name: example
      release_label: emr-6.6.0
      type: hive
      initial_capacity:
        initial_capacity_type: HiveDriver
        initial_capacity_config:
          worker_count: 1
          worker_configuration:
            cpu: 2 vCPU
            memory: 10 GB
```

## Maximum Capacity Usage

```yaml
resource:
  aws_emrserverless_application:
    example:
      name: example
      release_label: emr-6.6.0
      type: hive
      maximum_capacity:
        cpu: 2 vCPU
        memory: 10 GB
```

## Monitoring Configuration Usage

```yaml
resource:
  aws_emrserverless_application:
    example:
      name: example
      release_label: emr-7.1.0
      type: spark
      monitoring_configuration:
        cloudwatch_logging_configuration:
          enabled: true
          log_group_name: /aws/emr-serverless/example
          log_stream_name_prefix: spark-logs
          log_types:
            name: SPARK_DRIVER
            values: 
              - STDOUT
              - STDERR
          log_types:
            name: SPARK_EXECUTOR
            values: 
              - STDOUT
        managed_persistence_monitoring_configuration:
          enabled: true
        prometheus_monitoring_configuration:
          remote_write_url: "https://prometheus-remote-write-endpoint.example.com/api/v1/write"
```

## Runtime Configuration Usage

```yaml
resource:
  aws_emrserverless_application:
    example:
      name: example
      release_label: emr-6.8.0
      type: spark
      runtime_configuration:
        classification: spark-executor-log4j2
        properties: 
      runtime_configuration:
        classification: spark-defaults
        properties: 
```
