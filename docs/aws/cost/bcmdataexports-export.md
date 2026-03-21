# Bcmdataexports Export

Manage Bcmdataexports Export resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

resource:
  aws_bcmdataexports_export:
    test:
      export:
        name: testexample
        data_query:
          query_statement: SELECT identity_line_item_id, identity_time_interval, line_item_product_code,line_item_unblended_cost FROM COST_AND_USAGE_REPORT
          table_configurations:
            COST_AND_USAGE_REPORT:
              BILLING_VIEW_ARN: "arn:${data.aws_partition.current.partition}:billing::${data.aws_caller_identity.current.account_id}:billingview/primary"
              TIME_GRANULARITY: HOURLY
              INCLUDE_RESOURCES: FALSE
              INCLUDE_MANUAL_DISCOUNT_COMPATIBILITY: FALSE
              INCLUDE_SPLIT_COST_ALLOCATION_DATA: FALSE
        destination_configurations:
          s3_destination:
            s3_bucket: ${aws_s3_bucket.test.bucket}
            s3_prefix: ${aws_s3_bucket.test.bucket_prefix}
            s3_region: ${aws_s3_bucket.test.region}
            s3_output_configurations:
              overwrite: OVERWRITE_REPORT
              format: TEXT_OR_CSV
              compression: GZIP
              output_type: CUSTOM
        refresh_cadence:
          frequency: SYNCHRONOUS
```
