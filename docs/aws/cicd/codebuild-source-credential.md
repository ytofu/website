# Codebuild Source Credential

Manage Codebuild Source Credential resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codebuild_source_credential:
    example:
      auth_type: PERSONAL_ACCESS_TOKEN
      server_type: GITHUB
      token: example
```

## Bitbucket Server Usage

```yaml
resource:
  aws_codebuild_source_credential:
    example:
      auth_type: BASIC_AUTH
      server_type: BITBUCKET
      token: example
      user_name: test-user
```

## AWS CodeStar Connection Usage

```yaml
resource:
  aws_codebuild_source_credential:
    example:
      auth_type: CODECONNECTIONS
      server_type: GITHUB
      token: "arn:aws:codestar-connections:us-east-1:123456789012:connection/guid-string"
```
