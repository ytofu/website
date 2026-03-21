# Resource: aws_media_store_container_policy

Provides a MediaStore Container Policy.

## Basic Example

```yaml
data:
  aws_region:
    current:

  aws_caller_identity:
    current:

  aws_iam_policy_document:
    example:
      statement:
        sid: MediaStoreFullAccess
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - "arn:aws:iam::${data.aws_caller_identity.current.account_id}:root"
        actions: 
          - "mediastore:*"
        resources: 
          - "arn:aws:mediastore:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:container/${aws_media_store_container.example.name}/*"
        condition:
          test: Bool
          values: 
            - true

resource:
  aws_media_store_container:
    example:
      name: example

  aws_media_store_container_policy:
    example:
      container_name: ${aws_media_store_container.example.name}
      policy: ${data.aws_iam_policy_document.example.json}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `container_name` - (Required) The name of the container.
* `policy` - (Required) The contents of the policy. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy).

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_media_store_container_policy.example example
```
