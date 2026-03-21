# Codepipeline Webhook

Manage Codepipeline Webhook resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codepipeline:
    bar:
      name: tf-test-pipeline
      role_arn: ${aws_iam_role.bar.arn}
      artifact_store:
        location: ${aws_s3_bucket.bar.bucket}
        type: S3
        encryption_key:
          id: ${data.aws_kms_alias.s3kmskey.arn}
          type: KMS
      stage:
        name: Source
        action:
          name: Source
          category: Source
          owner: ThirdParty
          version: 1
          output_artifacts: 
            - test
          configuration:
            Owner: my-organization
            Repo: test
            Branch: master
      stage:
        name: Build
        action:
          name: Build
          category: Build
          owner: AWS
          input_artifacts: 
            - test
          version: 1
          configuration:
            ProjectName: test

resource:
  aws_codepipeline_webhook:
    bar:
      name: test-webhook-github-bar
      authentication: GITHUB_HMAC
      target_action: Source
      target_pipeline: ${aws_codepipeline.bar.name}
      authentication_configuration:
        secret_token: example-webhook_secret
      filter:
        json_path: $.ref
        match_equals: "refs/heads/{Branch}"

resource:
  github_repository_webhook:
    bar:
      repository: ${github_repository.repo.name}
      name: web
      configuration:
        url: ${aws_codepipeline_webhook.bar.url}
        content_type: json
        insecure_ssl: true
        secret: example-webhook_secret
      events: 
        - push
```
