# Resource: aws_codecommit_repository

Provides a CodeCommit Repository Resource.

## Basic Example

```yaml
resource:
  aws_codecommit_repository:
    test:
      repository_name: MyTestRepository
      description: This is the Sample App Repository
```

## AWS KMS Customer Managed Keys (CMK)

```yaml
resource:
  aws_codecommit_repository:
    test:
      repository_name: MyTestRepository
      description: This is the Sample App Repository
      kms_key_id: ${aws_kms_key.test.arn}

  aws_kms_key:
    test:
      description: test
      deletion_window_in_days: 7```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `repository_name` - (Required) The name for the repository. This needs to be less than 100 characters.
* `description` - (Optional) The description of the repository. This needs to be less than 1000 characters
* `default_branch` - (Optional) The default branch of the repository. The branch specified here needs to exist.
* `kms_key_id` - (Optional) The ARN of the encryption key. If no key is specified, the default `aws/codecommit` Amazon Web Services managed key is used.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `repository_id` - The ID of the repository
* `arn` - The ARN of the repository
* `clone_url_http` - The URL to use for cloning the repository over HTTPS.
* `clone_url_ssh` - The URL to use for cloning the repository over SSH.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_codecommit_repository.imported ExistingRepo
```
