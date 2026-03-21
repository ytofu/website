# Resource: aws_athena_data_catalog

Provides an Athena data catalog.

## Basic Example

```yaml
resource:
  aws_athena_data_catalog:
    example:
      name: athena-data-catalog
      description: Example Athena data catalog
      type: LAMBDA
      parameters: 
      tags:
        Name: example-athena-data-catalog
```

## Hive based Data Catalog

```yaml
resource:
  aws_athena_data_catalog:
    example:
      name: hive-data-catalog
      description: Hive based Data Catalog
      type: HIVE
      parameters: 
```

## Glue based Data Catalog

```yaml
resource:
  aws_athena_data_catalog:
    example:
      name: glue-data-catalog
      description: Glue based Data Catalog
      type: GLUE
      parameters: 
```

## Lambda based Data Catalog

```yaml
resource:
  aws_athena_data_catalog:
    example:
      name: lambda-data-catalog
      description: Lambda based Data Catalog
      type: LAMBDA
      parameters: 
```

## Argument Reference

This resource supports the following arguments:

- `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
- `name` - (Required) Name of the data catalog. The catalog name must be unique for the AWS account and can use a maximum of 128 alphanumeric, underscore, at sign, or hyphen characters.
- `type` - (Required) Type of data catalog: `LAMBDA` for a federated catalog, `GLUE` for AWS Glue Catalog, or `HIVE` for an external hive metastore.
- `parameters` - (Required) Key value pairs that specifies the Lambda function or functions to use for the data catalog. The mapping used depends on the catalog type.
- `description` - (Required) Description of the data catalog.
- `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

- `id` - Name of the data catalog.
- `arn` - ARN of the data catalog.
- `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_athena_data_catalog.example example-data-catalog
```
