# Resource: aws_organizations_organization

Provides a resource to create an organization.

## Basic Example

```yaml
resource:
  aws_organizations_organization:
    org:
      aws_service_access_principals:
        - cloudtrail.amazonaws.com
        - config.amazonaws.com
      feature_set: ALL
```

## Argument Reference

This resource supports the following arguments:

* `aws_service_access_principals` - (Optional) List of AWS service principal names for which you want to enable integration with your organization. This is typically in the form of a URL, such as service-abbreviation.amazonaws.com. Organization must have `feature_set` set to `ALL`. Some services do not support enablement via this endpoint, see [warning in aws docs](https://docs.aws.amazon.com/organizations/latest/APIReference/API_EnableAWSServiceAccess.html).
* `enabled_policy_types` - (Optional) List of Organizations policy types to enable in the Organization Root. Organization must have `feature_set` set to `ALL`. For additional information about valid policy types (e.g., `AISERVICES_OPT_OUT_POLICY`, `BACKUP_POLICY`, `BEDROCK_POLICY`, `CHATBOT_POLICY`, `DECLARATIVE_POLICY_EC2`, `INSPECTOR_POLICY`, `RESOURCE_CONTROL_POLICY`, `S3_POLICY`, `SECURITYHUB_POLICY`, `SERVICE_CONTROL_POLICY`, `TAG_POLICY` and `UPGRADE_ROLLOUT_POLICY`), see the [AWS Organizations API Reference](https://docs.aws.amazon.com/organizations/latest/APIReference/API_EnablePolicyType.html). To enable `INSPECTOR_POLICY`, `aws_service_access_principals` must include `inspector2.amazonaws.com`. To enable `SECURITYHUB_POLICY`, `aws_service_access_principals` must include `securityhub.amazonaws.com`.
* `feature_set` - (Optional) Specify `ALL` (default) or `CONSOLIDATED_BILLING`.
* `return_organization_only` - (Optional) Return (as attributes) only the results of the [`DescribeOrganization`](https://docs.aws.amazon.com/organizations/latest/APIReference/API_DescribeOrganization.html) API to avoid [API limits](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_reference_limits.html#throttling-limits). When configured to `true` only the `arn`, `feature_set`, `master_account_arn`, `master_account_email` and `master_account_id` attributes will be returned. All others will be empty. Default: `false`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `accounts` - List of organization accounts including the master account. For a list excluding the master account, see the `non_master_accounts` attribute. All elements have these attributes:
    * `arn` - ARN of the account.
    * `email` - Email of the account.
    * `id` - Identifier of the account.
    * `joined_method` - Method by which the account joined the organization.
    * `joined_timestamp` - Date the account became a part of the organization.
    * `name` - Name of the account.
    * `state` - State of the account.
* `arn` - ARN of the organization.
* `id` - Identifier of the organization.
* `master_account_arn` - ARN of the master account.
* `master_account_email` - Email address of the master account.
* `master_account_id` - Identifier of the master account.
* `master_account_name` - Name of the master account.
* `non_master_accounts` - List of organization accounts excluding the master account. For a list including the master account, see the `accounts` attribute. All elements have these attributes:
    * `arn` - ARN of the account.
    * `email` - Email of the account.
    * `id` - Identifier of the account.
    * `joined_method` - Method by which the account joined the organization.
    * `joined_timestamp` - Date the account became a part of the organization.
    * `name` - Name of the account.
    * `state` - State of the account.
* `roots` - List of organization roots. All elements have these attributes:
    * `arn` - ARN of the root.
    * `id` - Identifier of the root.
    * `name` - Name of the root.
    * `policy_types` - List of policy types enabled for this root. All elements have these attributes:
        * `name` - Name of the policy type.
        * `status` - Status of the policy type as it relates to the associated root.

## Import

```bash
ytofu import aws_organizations_organization.example o-1234567
```
