# Macie2 Classification Job

Manage Macie2 Classification Job resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_macie2_account:
    test:

resource:
  aws_macie2_classification_job:
    test:
      job_type: ONE_TIME
      name: NAME OF THE CLASSIFICATION JOB
      s3_job_definition:
        bucket_definitions:
          account_id: ACCOUNT ID
          buckets: 
            - S3 BUCKET NAME
      depends_on: 
        - ${aws_macie2_account.test}
```
