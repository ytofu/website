# Resource: aws_datazone_domain

ytofu resource for managing an AWS DataZone Domain.

## Basic Example

```yaml
resource:
  aws_iam_role:
    domain_execution_role:
      name: my_domain_execution_role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["sts:AssumeRole", "sts:TagSession"] "Effect": "Allow" "Principal": { "Service": "datazone.amazonaws.com" } }, { "Action": ["sts:AssumeRole", "sts:TagSession"] "Effect": "Allow" "Principal": { "Service": "cloudformation.amazonaws.com" } }, ] }'

  aws_iam_role_policy:
    domain_execution_role:
      role: ${aws_iam_role.domain_execution_role.name}
      policy: '{ "Version": "2012-10-17" "Statement": [ { # Consider scoping down "Action": [ "datazone:*", "ram:*", "sso:*", "kms:*", ] "Effect": "Allow" "Resource": "*" }, ] }'

  aws_datazone_domain:
    example:
      name: example
      domain_execution_role: ${aws_iam_role.domain_execution_role.arn}```

## V2 Domain

```yaml
data:
  aws_caller_identity:
    current:

  aws_iam_policy_document:
    assume_role_domain_execution:
      statement:
        actions:
          - "sts:AssumeRole"
          - "sts:TagSession"
          - "sts:SetContext"
        principals:
          type: Service
          identifiers: 
            - datazone.amazonaws.com
        condition:
          test: StringEquals
          values: 
            - ${data.aws_caller_identity.current.account_id}
        condition:
          test: "ForAllValues:StringLike"
          values: 
            - "datazone*"

  aws_iam_policy:
    domain_execution_role:
      name: SageMakerStudioDomainExecutionRolePolicy

  aws_iam_policy_document:
    assume_role_domain_service:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - datazone.amazonaws.com
        condition:
          test: StringEquals
          values: 
            - ${data.aws_caller_identity.current.account_id}

  aws_iam_policy:
    domain_service_role:
      name: SageMakerStudioDomainServiceRolePolicy

resource:
  aws_iam_role:
    domain_execution:
      assume_role_policy: ${data.aws_iam_policy_document.assume_role_domain_execution.json}
      name: example-domain-execution-role

  aws_iam_role_policy_attachment:
    domain_execution:
      policy_arn: ${data.aws_iam_policy.domain_execution_role.arn}
      role: ${aws_iam_role.domain_execution.name}

  aws_iam_role:
    domain_service:
      assume_role_policy: ${data.aws_iam_policy_document.assume_role_domain_service.json}
      name: example-domain-service-role

  aws_iam_role_policy_attachment:
    domain_service:
      policy_arn: ${data.aws_iam_policy.domain_service_role.arn}
      role: ${aws_iam_role.domain_service.name}

  aws_datazone_domain:
    example:
      name: example-domain
      domain_execution_role: ${aws_iam_role.domain_execution.arn}
      domain_version: V2
      service_role: ${aws_iam_role.domain_service.arn}```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the Domain.
* `domain_execution_role` - (Required) ARN of the role used by DataZone to configure the Domain.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the Domain.
* `domain_version` - (Optional) Version of the Domain. Valid values are `V1` and `V2`. Defaults to `V1`.
* `kms_key_identifier` - (Optional) ARN of the KMS key used to encrypt the Amazon DataZone domain, metadata and reporting data.
* `service_role` - (Optional) ARN of the service role used by DataZone. Required when `domain_version` is set to `V2`.
* `single_sign_on` - (Optional) Single sign on options, used to [enable AWS IAM Identity Center](https://docs.aws.amazon.com/datazone/latest/userguide/enable-IAM-identity-center-for-datazone.html) for DataZone.
* `skip_deletion_check` - (Optional) Whether to skip the deletion check for the Domain.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Domain.
* `id` - ID of the Domain.
* `portal_url` - URL of the data portal for the Domain.
* `root_domain_unit_id` - ID of the root domain unit.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `delete` - (Default `10m`)

## Import

```bash
ytofu import aws_datazone_domain.example domain-id-12345678
```
