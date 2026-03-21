# Cur Report Definition

Manage Cur Report Definition resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cur_report_definition:
    example_cur_report_definition:
      report_name: example-cur-report-definition
      time_unit: HOURLY
      format: textORcsv
      compression: GZIP
      additional_schema_elements: 
        - RESOURCES
        - SPLIT_COST_ALLOCATION_DATA
      s3_bucket: example-bucket-name
      s3_prefix: example-cur-report
      s3_region: us-east-1
      additional_artifacts: 
        - REDSHIFT
        - QUICKSIGHT
```
