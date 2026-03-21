# ECR Pull Through Cache Rule

Manage ECR Pull Through Cache Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecr_pull_through_cache_rule:
    example:
      ecr_repository_prefix: ecr-public
      upstream_registry_url: public.ecr.aws
      credential_arn: "arn:aws:secretsmanager:us-east-1:123456789:secret:ecr-pullthroughcache/ecrpublic"
```
