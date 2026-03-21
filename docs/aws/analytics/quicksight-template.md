# Quicksight Template

Manage Quicksight Template resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_template:
    example:
      template_id: example-id
      name: example-name
      version_description: version
      source_entity:
        source_template:
          arn: ${aws_quicksight_template.source.arn}
```

## With Definition

```yaml
resource:
  aws_quicksight_template:
    example:
      template_id: example-id
      name: example-name
      version_description: version
      definition:
        data_set_configuration:
          data_set_schema:
            column_schema_list:
              name: Column1
              data_type: STRING
            column_schema_list:
              name: Column2
              data_type: INTEGER
          placeholder: 1
        sheets:
          title: Test
          sheet_id: Test1
          visuals:
            bar_chart_visual:
              visual_id: BarChart
              chart_configuration:
                field_wells:
                  bar_chart_aggregated_field_wells:
                    category:
                      categorical_dimension_field:
                        field_id: 1
                        column:
                          column_name: Column1
                          data_set_identifier: 1
                    values:
                      numerical_measure_field:
                        field_id: 2
                        column:
                          column_name: Column2
                          data_set_identifier: 1
                        aggregation_function:
                          simple_numerical_aggregation: SUM
```
