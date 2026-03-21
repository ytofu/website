# Lakeformation Permissions

Manage Lakeformation Permissions resources using ytofu YAML.

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
