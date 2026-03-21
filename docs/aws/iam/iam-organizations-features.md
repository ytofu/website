# Resource: aws_iam_organizations_features

Manages centralized root access features across AWS member accounts managed using AWS Organizations. More information about managing root access in IAM can be found in the [Centralize root access for member accounts](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-enable-root-access.html).

## Basic Example

```yaml
resource:
  aws_organizations_organization:
    example:
      aws_service_access_principals: 
        - iam.amazonaws.com
      feature_set: ALL

resource:
  aws_iam_organizations_features:
    example:
      enabled_features:
        - RootCredentialsManagement
        - RootSessions
```

## Argument Reference

The following arguments are required:

* `enabled_features` - (Required) List of IAM features to enable. Valid values are `RootCredentialsManagement` and `RootSessions`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - AWS Organization identifier.

## Import

```bash
ytofu import aws_iam_organizations_features.example o-1234567
```
