# Resource: aws_lakeformation_lf_tag_expression

ytofu resource for managing an AWS Lake Formation LF Tag Expression.

## Basic Example

```yaml
resource:
  aws_lakeformation_lf_tag:
    example:
      key: example
      values: 
        - value

  aws_lakeformation_lf_tag_expression:
    example:
      name: example
      expression:
        tag_key: ${aws_lakeformation_lf_tag.example.key}
        tag_values: ${aws_lakeformation_lf_tag.example.values}```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the LF-Tag Expression.
* `expression` - (Required) A list of LF-Tag conditions (key-value pairs). See [expression](#expression) for more details.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `catalog_id` - (Optional) ID of the Data Catalog. Defaults to the account ID if not specified.
* `description` - (Optional) Description of the LF-Tag Expression.

### expression

* `tag_key` - (Required) The key-name for the LF-Tag.
* `tag_values` - (Required) A list of possible values for the LF-Tag

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_lakeformation_lf_tag_expression.example example-tag-expression,123456789012
```
