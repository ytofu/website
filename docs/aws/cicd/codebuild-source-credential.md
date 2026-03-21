# Resource: aws_codebuild_source_credential

Provides a CodeBuild Source Credentials Resource.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `auth_type` - (Required) The type of authentication used to connect to a GitHub, GitHub Enterprise, or Bitbucket
  repository. Valid values are `BASIC_AUTH`,
  `PERSONAL_ACCESS_TOKEN`, `CODECONNECTIONS`, and `SECRETS_MANAGER`. An OAUTH connection is not supported by the API.
* `server_type` - (Required) The source provider used for this project.
* `token` - (Required) For a GitHub and GitHub Enterprise, this is the personal access token. For Bitbucket, this is the
  app password. When using an AWS CodeStar connection (`auth_type = "CODECONNECTIONS")`, this is an AWS CodeStar
  Connection ARN.
* `user_name` - (Optional) The Bitbucket username when the authType is `BASIC_AUTH`. This parameter is not valid for
  other types of source providers or connections.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ARN of Source Credential.
* `arn` - The ARN of Source Credential.

## Import

```bash
ytofu import aws_codebuild_source_credential.example arn:aws:codebuild:us-west-2:123456789:token:github
```
