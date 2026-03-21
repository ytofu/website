# Resource: aws_codeartifact_repository_permissions_policy

Provides a CodeArtifact Repostory Permissions Policy Resource.

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
    example:
      repository: example
      domain: ${aws_codeartifact_domain.example.domain}

  aws_codeartifact_repository_permissions_policy:
    example:
      repository: ${aws_codeartifact_repository.example.repository}
      domain: ${aws_codeartifact_domain.example.domain}
      policy_document: ${data.aws_iam_policy_document.example.json}

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        principals:
          type: "*"
          identifiers: 
            - "*"
        actions: 
          - "codeartifact:ReadFromRepository"
        resources: 
          - ${aws_codeartifact_repository.example.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `repository` - (Required) The name of the repository to set the resource policy on.
* `domain` - (Required) The name of the domain on which to set the resource policy.
* `policy_document` - (Required) A JSON policy string to be set as the access control resource policy on the provided domain.
* `domain_owner` - (Optional) The account number of the AWS account that owns the domain.
* `policy_revision` - (Optional) The current revision of the resource policy to be set. This revision is used for optimistic locking, which prevents others from overwriting your changes to the domain's resource policy.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ARN of the resource associated with the resource policy.
* `resource_arn` - The ARN of the resource associated with the resource policy.

## Import

```bash
ytofu import aws_codeartifact_repository_permissions_policy.example arn:aws:codeartifact:us-west-2:012345678912:repository/tf-acc-test-6968272603913957763/tf-acc-test-6968272603913957763
```
