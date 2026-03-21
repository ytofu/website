# Resource: aws_ses_identity_policy

Manages a SES Identity Policy. More information about SES Sending Authorization Policies can be found in the [SES Developer Guide](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/sending-authorization-policies.html).

## Basic Example

```yaml
resource:
  aws_ses_domain_identity:
    example:
      domain: example.com

  aws_ses_identity_policy:
    example:
      identity: ${aws_ses_domain_identity.example.arn}
      name: example
      policy: ${data.aws_iam_policy_document.example.json}

data:
  aws_iam_policy_document:
    example:
      statement:
        actions: 
          - "SES:SendEmail"
          - "SES:SendRawEmail"
        resources: 
          - ${aws_ses_domain_identity.example.arn}
        principals:
          identifiers: 
            - "*"
          type: AWS```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `identity` - (Required) Name or Amazon Resource Name (ARN) of the SES Identity.
* `name` - (Required) Name of the policy.
* `policy` - (Required) JSON string of the policy. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy).

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_ses_identity_policy.example 'example.com|example'
```
