# Resource: aws_lakeformation_data_lake_settings

Manages Lake Formation principals designated as data lake administrators and lists of principal permission entries for default create database and default create table permissions.

## Basic Example

```yaml
resource:
  aws_lakeformation_data_lake_settings:
    example:
      admins: 
        - ${aws_iam_user.test.arn}
        - ${aws_iam_role.test.arn}
```

## Create Default Permissions

```yaml
resource:
  aws_lakeformation_data_lake_settings:
    example:
      admins: 
        - ${aws_iam_user.test.arn}
        - ${aws_iam_role.test.arn}
      create_database_default_permissions:
        permissions: 
          - SELECT
          - ALTER
          - DROP
        principal: ${aws_iam_user.test.arn}
      create_table_default_permissions:
        permissions: 
          - ALL
        principal: ${aws_iam_role.test.arn}
```

## Enable EMR access to LakeFormation resources

```yaml
resource:
  aws_lakeformation_data_lake_settings:
    example:
      admins: 
        - ${aws_iam_user.test.arn}
        - ${aws_iam_role.test.arn}
      create_database_default_permissions:
        permissions: 
          - SELECT
          - ALTER
          - DROP
        principal: ${aws_iam_user.test.arn}
      create_table_default_permissions:
        permissions: 
          - ALL
        principal: ${aws_iam_role.test.arn}
      allow_external_data_filtering: true
      external_data_filtering_allow_list: 
        - ${data.aws_caller_identity.current.account_id}
        - ${data.aws_caller_identity.third_party.account_id}
      authorized_session_tag_value_list: 
        - Amazon EMR
      allow_full_table_external_data_access: true
```

## Change Cross Account Version

```yaml
resource:
  aws_lakeformation_data_lake_settings:
    example:
      parameters: 
```

## Argument Reference

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `admins` - (Optional) Set of ARNs of AWS Lake Formation principals (IAM users or roles).
* `allow_external_data_filtering` - (Optional) Whether to allow Amazon EMR clusters to access data managed by Lake Formation.
* `allow_full_table_external_data_access` - (Optional) Whether to allow a third-party query engine to get data access credentials without session tags when a caller has full data access permissions.
* `authorized_session_tag_value_list` - (Optional) Lake Formation relies on a privileged process secured by Amazon EMR or the third party integrator to tag the user's role while assuming it.
* `catalog_id` - (Optional) Identifier for the Data Catalog. By default, the account ID.
* `create_database_default_permissions` - (Optional) Up to three configuration blocks of principal permissions for default create database permissions. Detailed below.
* `create_table_default_permissions` - (Optional) Up to three configuration blocks of principal permissions for default create table permissions. Detailed below.
* `external_data_filtering_allow_list` - (Optional) A list of the account IDs of Amazon Web Services accounts with Amazon EMR clusters that are to perform data filtering.
* `parameters` - Key-value map of additional configuration. Valid values for the `CROSS_ACCOUNT_VERSION` key are `"1"`, `"2"`, `"3"`, or `"4"`. `SET_CONTEXT` is also returned with a value of `TRUE`. In a fresh account, prior to configuring, `CROSS_ACCOUNT_VERSION` is `"1"`. Destroying this resource sets the `CROSS_ACCOUNT_VERSION` to `"1"`.
* `read_only_admins` - (Optional) Set of ARNs of AWS Lake Formation principals (IAM users or roles) with only view access to the resources.
* `trusted_resource_owners` - (Optional) List of the resource-owning account IDs that the caller's account can use to share their user access details (user ARNs).

### create_database_default_permissions

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `permissions` - (Optional) List of permissions that are granted to the principal. Valid values may include `ALL`, `SELECT`, `ALTER`, `DROP`, `DELETE`, `INSERT`, `DESCRIBE`, and `CREATE_TABLE`. For more details, see [Lake Formation Permissions Reference](https://docs.aws.amazon.com/lake-formation/latest/dg/lf-permissions-reference.html).
* `principal` - (Optional) Principal who is granted permissions. To enforce metadata and underlying data access control only by IAM on new databases and tables set `principal` to `IAM_ALLOWED_PRINCIPALS` and `permissions` to `["ALL"]`.

### create_table_default_permissions

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `permissions` - (Optional) List of permissions that are granted to the principal. Valid values may include `ALL`, `SELECT`, `ALTER`, `DROP`, `DELETE`, `INSERT`, and `DESCRIBE`. For more details, see [Lake Formation Permissions Reference](https://docs.aws.amazon.com/lake-formation/latest/dg/lf-permissions-reference.html).
* `principal` - (Optional) Principal who is granted permissions. To enforce metadata and underlying data access control only by IAM on new databases and tables set `principal` to `IAM_ALLOWED_PRINCIPALS` and `permissions` to `["ALL"]`.

## Attribute Reference

This resource exports no additional attributes.
