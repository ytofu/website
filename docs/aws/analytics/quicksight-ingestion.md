# Resource: aws_quicksight_ingestion

ytofu resource for managing an AWS QuickSight Ingestion.

## Basic Example

```yaml
resource:
  aws_quicksight_ingestion:
    example:
      data_set_id: ${aws_quicksight_data_set.example.data_set_id}
      ingestion_id: example-id
      ingestion_type: FULL_REFRESH
```

## Argument Reference

The following arguments are required:

* `data_set_id` - (Required) ID of the dataset used in the ingestion.
* `ingestion_id` - (Required) ID for the ingestion.
* `ingestion_type` - (Required) Type of ingestion to be created. Valid values are `INCREMENTAL_REFRESH` and `FULL_REFRESH`.

The following arguments are optional:

* `aws_account_id` - (Optional, Forces new resource) AWS account ID. Defaults to automatically determined account ID of the ytofu AWS provider.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Ingestion.
* `id` - A comma-delimited string joining AWS account ID, data set ID, and ingestion ID.
* `ingestion_status` - Ingestion status.

## Import

```bash
ytofu import aws_quicksight_ingestion.example 123456789012,example-dataset-id,example-ingestion-id
```
