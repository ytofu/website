# Resource: aws_resourceexplorer2_view

Provides a resource to manage a Resource Explorer view.

## Basic Example

```yaml
resource:
  aws_resourceexplorer2_index:
    example:
      type: LOCAL

resource:
  aws_resourceexplorer2_view:
    example:
      name: exampleview
      filters:
        filter_string: "resourcetype:ec2:instance"
      included_property:
        name: tags
      depends_on: 
        - ${aws_resourceexplorer2_index.example}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `default_view` - (Optional) Specifies whether the view is the [_default view_](https://docs.aws.amazon.com/resource-explorer/latest/userguide/manage-views-about.html#manage-views-about-default) for the AWS Region. Default: `false`.
* `filters` - (Optional) Specifies which resources are included in the results of queries made using this view. See [Filters](#filters) below for more details.
* `included_property` - (Optional) Optional fields to be included in search results from this view. See [Included Properties](#included-properties) below for more details.
* `name` - (Required) The name of the view. The name must be no more than 64 characters long, and can include letters, digits, and the dash (-) character. The name must be unique within its AWS Region.
* `scope`- (Optional) The root ARN of the account, an organizational unit (OU), or an organization ARN. If left empty, the default is account.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### Filters

The `filters` block supports the following:

* `filter_string` - (Required) The string that contains the search keywords, prefixes, and operators to control the results that can be returned by a search operation. For more details, see [Search query syntax](https://docs.aws.amazon.com/resource-explorer/latest/userguide/using-search-query-syntax.html).

### Included Properties

The `included_property` block supports the following:

* `name` - (Required) The name of the property that is included in this view. Valid values: `tags`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of the Resource Explorer view.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_resourceexplorer2_view.example arn:aws:resource-explorer-2:us-west-2:123456789012:view/exampleview/e0914f6c-6c27-4b47-b5d4-6b28381a2421
```
