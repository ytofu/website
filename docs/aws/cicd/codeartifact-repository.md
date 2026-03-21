# Resource: aws_codeartifact_repository

Provides a CodeArtifact Repository Resource.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:
      description: domain key

  aws_codeartifact_domain:
    example:
      domain: example
      encryption_key: ${aws_kms_key.example.arn}

  aws_codeartifact_repository:
    test:
      repository: example
      domain: ${aws_codeartifact_domain.example.domain}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `domain` - (Required) The domain that contains the created repository.
* `repository` - (Required) The name of the repository to create.
* `domain_owner` - (Optional) The account number of the AWS account that owns the domain.
* `description` - (Optional) The description of the repository.
* `upstream` - (Optional) A list of upstream repositories to associate with the repository. The order of the upstream repositories in the list determines their priority order when AWS CodeArtifact looks for a requested package version. see [Upstream](#upstream)
* `external_connections` - An array of external connections associated with the repository. Only one external connection can be set per repository. see [External Connections](#external-connections).
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### Upstream

* `repository_name` - (Required) The name of an upstream repository.

### External Connections

* `external_connection_name` - (Required) The name of the external connection associated with a repository.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ARN of the repository.
* `arn` - The ARN of the repository.
* `administrator_account` - The account number of the AWS account that manages the repository.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_codeartifact_repository.example arn:aws:codeartifact:us-west-2:012345678912:repository/tf-acc-test-6968272603913957763/tf-acc-test-6968272603913957763
```
