# Glue Classifier

Manage Glue Classifier resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_glue_classifier:
    example:
      name: example
      csv_classifier:
        allow_single_column: false
        contains_header: PRESENT
        delimiter: ","
        disable_value_trimming: false
        header: 
          - example1
          - example2
        quote_symbol: "'"
```

## Grok Classifier

```yaml
resource:
  aws_glue_classifier:
    example:
      name: example
      grok_classifier:
        classification: example
        grok_pattern: example
```

## JSON Classifier

```yaml
resource:
  aws_glue_classifier:
    example:
      name: example
      json_classifier:
        json_path: example
```

## XML Classifier

```yaml
resource:
  aws_glue_classifier:
    example:
      name: example
      xml_classifier:
        classification: example
        row_tag: example
```
