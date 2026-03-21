# Resource: aws_lakeformation_permissions

Grants permissions to the principal to access metadata in the Data Catalog and data organized in underlying data storage such as Amazon S3. Permissions are granted to a principal, in a Data Catalog, relative to a Lake Formation resource, which includes the Data Catalog, databases, tables, LF-tags, and LF-tag policies. For more information, see [Security and Access Control to Metadata and Data in Lake Formation](https://docs.aws.amazon.com/lake-formation/latest/dg/security-data-access.html).

## Basic Example

```yaml
resource:
  aws_lakeformation_permissions:
    example:
      principal: ${aws_iam_role.workflow_role.arn}
      permissions: 
        - DATA_LOCATION_ACCESS
      data_location:
        arn: ${aws_lakeformation_resource.example.arn}
```

## Grant Permissions For A Glue Catalog Database

```yaml
resource:
  aws_lakeformation_permissions:
    example:
      principal: ${aws_iam_role.workflow_role.arn}
      permissions: 
        - CREATE_TABLE
        - ALTER
        - DROP
      database:
        name: ${aws_glue_catalog_database.example.name}
        catalog_id: 110376042874
```

## Grant Permissions Using Tag-Based Access Control

```yaml
resource:
  aws_lakeformation_permissions:
    test:
      principal: ${aws_iam_role.sales_role.arn}
      permissions: 
        - CREATE_TABLE
        - ALTER
        - DROP
      lf_tag_policy:
        resource_type: DATABASE
        expression:
          key: Team
          values: 
            - Sales
        expression:
          key: Environment
          values: 
            - Dev
            - Production
```

## Argument Reference

The following arguments are required:

* `permissions` - (Required) List of permissions granted to the principal. Valid values may include `ALL`, `ALTER`, `ASSOCIATE`, `CREATE_DATABASE`, `CREATE_TABLE`, `DATA_LOCATION_ACCESS`, `DELETE`, `DESCRIBE`, `DROP`, `INSERT`, and `SELECT`. For details on each permission, see [Lake Formation Permissions Reference](https://docs.aws.amazon.com/lake-formation/latest/dg/lf-permissions-reference.html).
* `principal` - (Required) Principal to be granted the permissions on the resource. Supported principals include `IAM_ALLOWED_PRINCIPALS` (see [Default Behavior and `IAMAllowedPrincipals`](#default-behavior-and-iamallowedprincipals) above), IAM roles, users, groups, Federated Users, SAML groups and users, QuickSight groups, OUs, and organizations as well as AWS account IDs for cross-account permissions. For more information, see [Lake Formation Permissions Reference](https://docs.aws.amazon.com/lake-formation/latest/dg/lf-permissions-reference.html).

One of the following is required:

* `catalog_resource` - (Optional) Whether the permissions are to be granted for the Data Catalog. Defaults to `false`.
* `data_cells_filter` - (Optional) Configuration block for a data cells filter resource. Detailed below.
* `data_location` - (Optional) Configuration block for a data location resource. Detailed below.
* `database` - (Optional) Configuration block for a database resource. Detailed below.
* `lf_tag` - (Optional) Configuration block for an LF-tag resource. Detailed below.
* `lf_tag_policy` - (Optional) Configuration block for an LF-tag policy resource. Detailed below.
* `table` - (Optional) Configuration block for a table resource. Detailed below.
* `table_with_columns` - (Optional) Configuration block for a table with columns resource. Detailed below.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `catalog_id` - (Optional) Identifier for the Data Catalog. By default, the account ID. The Data Catalog is the persistent metadata store. It contains database definitions, table definitions, and other control information to manage your Lake Formation environment.
* `permissions_with_grant_option` - (Optional) Subset of `permissions` which the principal can pass.

### data_cells_filter

* `database_name` - (Required) The name of the database.
* `name` - (Required) The name of the data cells filter.
* `table_catalog_id` - (Required) The ID of the Data Catalog.
* `table_name` - (Required) The name of the table.

### data_location

The following argument is required:

* `arn` - (Required) Amazon Resource Name (ARN) that uniquely identifies the data location resource.

The following argument is optional:

* `catalog_id` - (Optional) Identifier for the Data Catalog where the location is registered with Lake Formation. By default, it is the account ID of the caller.

### database

The following argument is required:

* `name` - (Required) Name of the database resource. Unique to the Data Catalog.

The following argument is optional:

* `catalog_id` - (Optional) Identifier for the Data Catalog. By default, it is the account ID of the caller.

### lf_tag

The following arguments are required:

* `key` - (Required) The key-name for the tag.
* `values` - (Required) A list of possible values an attribute can take.

The following argument is optional:

* `catalog_id` - (Optional) Identifier for the Data Catalog. By default, it is the account ID of the caller.

### lf_tag_policy

The following arguments are required:

* `resource_type` - (Required) The resource type for which the tag policy applies. Valid values are `DATABASE` and `TABLE`.
* `expression` - (Required) A list of tag conditions that apply to the resource's tag policy. Configuration block for tag conditions that apply to the policy. See [`expression`](#expression) below.

The following argument is optional:

* `catalog_id` - (Optional) Identifier for the Data Catalog. By default, it is the account ID of the caller.

#### expression

* `key` - (Required) The key-name of an LF-Tag.
* `values` - (Required) A list of possible values of an LF-Tag.

### table

The following argument is required:

* `database_name` - (Required) Name of the database for the table. Unique to a Data Catalog.
* `name` - (Required, at least one of `name` or `wildcard`) Name of the table.
* `wildcard` - (Required, at least one of `name` or `wildcard`) Whether to use a wildcard representing every table under a database. Defaults to `false`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `catalog_id` - (Optional) Identifier for the Data Catalog. By default, it is the account ID of the caller.

### table_with_columns

The following arguments are required:

* `column_names` - (Required, at least one of `column_names` or `wildcard`) Set of column names for the table.
* `database_name` - (Required) Name of the database for the table with columns resource. Unique to the Data Catalog.
* `name` - (Required) Name of the table resource.
* `wildcard` - (Required, at least one of `column_names` or `wildcard`) Whether to use a column wildcard. If `excluded_column_names` is included, `wildcard` must be set to `true` to avoid ytofu reporting a difference.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `catalog_id` - (Optional) Identifier for the Data Catalog. By default, it is the account ID of the caller.
* `excluded_column_names` - (Optional) Set of column names for the table to exclude. If `excluded_column_names` is included, `wildcard` must be set to `true` to avoid ytofu reporting a difference.

## Attribute Reference

This resource exports no additional attributes.
