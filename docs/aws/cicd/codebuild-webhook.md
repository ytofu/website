# Resource: aws_codebuild_webhook

Manages a CodeBuild webhook, which is an endpoint accepted by the CodeBuild service to trigger builds from source code repositories. Depending on the source type of the CodeBuild project, the CodeBuild service may also automatically create and delete the actual repository webhook as well.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `project_name` - (Required) The name of the build project.
* `build_type` - (Optional) The type of build this webhook will trigger. Valid values for this parameter are: `BUILD`, `BUILD_BATCH`.
* `manual_creation` - (Optional) If true, CodeBuild doesn't create a webhook in GitHub and instead returns `payload_url` and `secret` values for the webhook. The `payload_url` and `secret` values in the output can be used to manually create a webhook within GitHub.
* `branch_filter` - (Optional) A regular expression used to determine which branches get built. Default is all branches are built. We recommend using `filter_group` over `branch_filter`.
* `filter_group` - (Optional) Information about the webhook's trigger. See [filter_group](#filter_group) for details.
* `scope_configuration` - (Optional) Scope configuration for global or organization webhooks. See [scope_configuration](#scope_configuration) for details.
* `pull_request_build_policy` - (Optional) Defines comment-based approval requirements for triggering builds on pull requests. See [pull_request_build_policy](#pull_request_build_policy) for details.

### filter_group

* `filter` - (Required) A webhook filter for the group. See [filter](#filter) for details.

### filter

* `type` - (Required) The webhook filter group's type. Valid values for this parameter are: `EVENT`, `BASE_REF`, `HEAD_REF`, `ACTOR_ACCOUNT_ID`, `FILE_PATH`, `COMMIT_MESSAGE`, `WORKFLOW_NAME`, `TAG_NAME`, `RELEASE_NAME`, `REPOSITORY_NAME`. At least one filter group must specify `EVENT` as its type.
* `pattern` - (Required) For a filter that uses `EVENT` type, a comma-separated string that specifies one event: `PUSH`, `PULL_REQUEST_CREATED`, `PULL_REQUEST_UPDATED`, `PULL_REQUEST_REOPENED`. `PULL_REQUEST_MERGED`, `WORKFLOW_JOB_QUEUED` works with GitHub & GitHub Enterprise only. For a filter that uses any of the other filter types, a regular expression.
* `exclude_matched_pattern` - (Optional) If set to `true`, the specified filter does *not* trigger a build. Defaults to `false`.

### scope_configuration

* `name` - (Required) The name of either the enterprise or organization.
* `scope` - (Required) The type of scope for a GitHub webhook. Valid values for this parameter are: `GITHUB_ORGANIZATION`, `GITHUB_GLOBAL`.
* `domain` - (Optional) The domain of the GitHub Enterprise organization. Required if your project's source type is GITHUB_ENTERPRISE.

### pull_request_build_policy

* `requires_comment_approval` - (Required) Specifies when comment-based approval is required before triggering a build on pull requests. Valid values are: `DISABLED`, `ALL_PULL_REQUESTS`, and `FORK_PULL_REQUESTS`.
* `approver_roles` - (Optional) List of repository roles that have approval privileges for pull request builds when comment approval is required. This argument must be specified only when `requires_comment_approval` is not `DISABLED`. See the [AWS documentation](https://docs.aws.amazon.com/codebuild/latest/userguide/pull-request-build-policy.html#pull-request-build-policy.configuration) for valid values and defaults.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the build project.
* `payload_url` - The CodeBuild endpoint where webhook events are sent.
* `secret` - The secret token of the associated repository. Not returned by the CodeBuild API for all source types.
* `url` - The URL to the webhook.

## Import

```bash
ytofu import aws_codebuild_webhook.example MyProjectName
```
