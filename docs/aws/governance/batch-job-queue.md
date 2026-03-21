# Batch Job Queue

Manage Batch Job Queue resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_batch_job_queue:
    test_queue:
      name: tf-test-batch-job-queue
      state: ENABLED
      priority: 1
      compute_environment_order:
        order: 1
        compute_environment: ${aws_batch_compute_environment.test_environment_1.arn}
      compute_environment_order:
        order: 2
        compute_environment: ${aws_batch_compute_environment.test_environment_2.arn}
```

## Job Queue with a fair share scheduling policy

```yaml
resource:
  aws_batch_scheduling_policy:
    example:
      name: example
      fair_share_policy:
        compute_reservation: 1
        share_decay_seconds: 3600
        share_distribution:
          share_identifier: "A1*"
          weight_factor: 0.1

resource:
  aws_batch_job_queue:
    example:
      name: tf-test-batch-job-queue
      scheduling_policy_arn: ${aws_batch_scheduling_policy.example.arn}
      state: ENABLED
      priority: 1
      compute_environment_order:
        order: 1
        compute_environment: ${aws_batch_compute_environment.test_environment_1.arn}
      compute_environment_order:
        order: 2
        compute_environment: ${aws_batch_compute_environment.test_environment_2.arn}
```
