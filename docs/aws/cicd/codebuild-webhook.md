# Codebuild Webhook

Manage Codebuild Webhook resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codebuild_webhook:
    example:
      project_name: ${aws_codebuild_project.example.name}
      build_type: BUILD
      filter_group:
        filter:
          type: EVENT
          pattern: PUSH
        filter:
          type: BASE_REF
          pattern: master
```

## GitHub Enterprise

```yaml
resource:
  aws_codebuild_webhook:
    example:
      project_name: ${aws_codebuild_project.example.name}

resource:
  github_repository_webhook:
    example:
      active: true
      events: 
        - push
      name: example
      repository: ${github_repository.example.name}
      configuration:
        url: ${aws_codebuild_webhook.example.payload_url}
        secret: ${aws_codebuild_webhook.example.secret}
        content_type: json
        insecure_ssl: false
```

## For CodeBuild Runner Project

```yaml
resource:
  aws_codebuild_webhook:
    example:
      project_name: ${aws_codebuild_project.example.name}
      build_type: BUILD
      filter_group:
        filter:
          type: EVENT
          pattern: WORKFLOW_JOB_QUEUED
```
