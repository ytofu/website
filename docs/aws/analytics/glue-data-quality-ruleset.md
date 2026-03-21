# Resource: aws_glue_data_quality_ruleset

Provides a Glue Data Quality Ruleset Resource. You can refer to the [Glue Developer Guide](https://docs.aws.amazon.com/glue/latest/dg/glue-data-quality.html) for a full explanation of the Glue Data Quality Ruleset functionality

## Basic Example

```yaml
resource:
  aws_glue_data_quality_ruleset:
    example:
      name: example
      ruleset: Rules = [Completeness \"colA\" between 0.4 and 0.8]
```

## With description

```yaml
resource:
  aws_glue_data_quality_ruleset:
    example:
      name: example
      description: example
      ruleset: Rules = [Completeness \"colA\" between 0.4 and 0.8]
```

## With tags

```yaml
resource:
  aws_glue_data_quality_ruleset:
    example:
      name: example
      ruleset: Rules = [Completeness \"colA\" between 0.4 and 0.8]
      tags: 
```

## With target_table

```yaml
resource:
  aws_glue_data_quality_ruleset:
    example:
      name: example
      ruleset: Rules = [Completeness \"colA\" between 0.4 and 0.8]
      target_table:
        database_name: ${aws_glue_catalog_database.example.name}
        table_name: ${aws_glue_catalog_table.example.name}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Description of the data quality ruleset.
* `name` - (Required, Forces new resource) Name of the data quality ruleset.
* `ruleset` - (Optional) A Data Quality Definition Language (DQDL) ruleset. For more information, see the AWS Glue developer guide.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `target_table` - (Optional, Forces new resource) A Configuration block specifying a target table associated with the data quality ruleset. See [`target_table`](#target_table) below.

### target_table

* `catalog_id` - (Optional, Forces new resource) The catalog id where the AWS Glue table exists.
* `database_name` - (Required, Forces new resource) Name of the database where the AWS Glue table exists.
* `table_name` - (Required, Forces new resource) Name of the AWS Glue table.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Glue Data Quality Ruleset.
* `created_on` - The time and date that this data quality ruleset was created.
* `last_modified_on` - The time and date that this data quality ruleset was created.
* `recommendation_run_id` - When a ruleset was created from a recommendation run, this run ID is generated to link the two together.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_glue_data_quality_ruleset.example exampleName
```
