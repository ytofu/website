# Kendra Data Source

Manage Kendra Data Source resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kendra_data_source:
    example:
      index_id: ${aws_kendra_index.example.id}
      name: example
      description: example
      language_code: en
      type: CUSTOM
      tags: 
```

## S3 Connector

```yaml
resource:
  aws_kendra_data_source:
    example:
      index_id: ${aws_kendra_index.example.id}
      name: example
      type: S3
      role_arn: ${aws_iam_role.example.arn}
      schedule: "cron(9 10 1 * ? *)"
      configuration:
        s3_configuration:
          bucket_name: ${aws_s3_bucket.example.id}
```

## Web Crawler Connector

```yaml
resource:
  aws_kendra_data_source:
    example:
      index_id: ${aws_kendra_index.example.id}
      name: example
      type: WEBCRAWLER
      role_arn: ${aws_iam_role.example.arn}
      configuration:
        web_crawler_configuration:
          urls:
            seed_url_configuration:
              seed_urls:
                - REPLACE_WITH_YOUR_URL
```
