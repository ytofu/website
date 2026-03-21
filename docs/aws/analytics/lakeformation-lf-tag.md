# Resource: aws_lakeformation_lf_tag

Creates an LF-Tag with the specified name and values. Each key must have at least one value. The maximum number of values permitted is 1000.

## Basic Example

```yaml
resource:
  aws_lakeformation_lf_tag:
    example:
      key: module
      values: 
        - Orders
        - Sales
        - Customers
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `catalog_id` - (Optional) ID of the Data Catalog to create the tag in. If omitted, this defaults to the AWS Account ID.
* `key` - (Required) Key-name for the tag.
* `values` - (Required) List of possible values an attribute can take.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Catalog ID and key-name of the tag

## Import

```bash
ytofu import aws_lakeformation_lf_tag.example 123456789012:some_key
```
