# Glue Trigger

Manage Glue Trigger resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_trigger:
    example:
      name: example
      type: CONDITIONAL
      actions:
        job_name: ${aws_glue_job.example1.name}
      predicate:
        conditions:
          job_name: ${aws_glue_job.example2.name}
          state: SUCCEEDED
```

## On-Demand Trigger

```yaml
resource:
  aws_glue_trigger:
    example:
      name: example
      type: ON_DEMAND
      actions:
        job_name: ${aws_glue_job.example.name}
```

## Scheduled Trigger

```yaml
resource:
  aws_glue_trigger:
    example:
      name: example
      schedule: "cron(15 12 * * ? *)"
      type: SCHEDULED
      actions:
        job_name: ${aws_glue_job.example.name}
```

## Conditional Trigger with Crawler Action

```yaml
resource:
  aws_glue_trigger:
    example:
      name: example
      type: CONDITIONAL
      actions:
        crawler_name: ${aws_glue_crawler.example1.name}
      predicate:
        conditions:
          job_name: ${aws_glue_job.example2.name}
          state: SUCCEEDED
```

## Conditional Trigger with Crawler Condition

```yaml
resource:
  aws_glue_trigger:
    example:
      name: example
      type: CONDITIONAL
      actions:
        job_name: ${aws_glue_job.example1.name}
      predicate:
        conditions:
          crawler_name: ${aws_glue_crawler.example2.name}
          crawl_state: SUCCEEDED
```
