# Resource: aws_workspaces_ip_group

Provides an IP access control group in AWS WorkSpaces Service

## Basic Example

```yaml
resource:
  aws_workspaces_ip_group:
    contractors:
      name: Contractors
      description: Contractors IP access control group
      rules:
        source: 150.24.14.0/24
        description: NY
      rules:
        source: 125.191.14.85/32
        description: LA
      rules:
        source: 44.98.100.0/24
        description: STL
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the IP group.
* `description` - (Optional) The description of the IP group.
* `rules` - (Optional) One or more pairs specifying the IP group rule (in CIDR format) from which web requests originate.
* `tags` - (Optional) A map of tags assigned to the WorkSpaces directory. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The IP group identifier.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_workspaces_ip_group.example wsipg-488lrtl3k
```
