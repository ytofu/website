# Codestarconnections Connection

Manage Codestarconnections Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codestarconnections_connection:
    example:
      name: example-connection
      provider_type: Bitbucket

resource:
  aws_codepipeline:
    example:
      name: tf-test-pipeline
      role_arn: ${aws_iam_role.codepipeline_role.arn}
      artifact_store:
      stage:
        name: Source
        action:
          name: Source
          category: Source
          owner: AWS
          version: 1
          output_artifacts: 
            - source_output
          configuration:
            ConnectionArn: ${aws_codestarconnections_connection.example.arn}
            FullRepositoryId: my-organization/test
            BranchName: main
      stage:
        name: Build
        action:
      stage:
        name: Deploy
        action:
```
