# Resource: aws_route53_resolver_firewall_domain_list

Provides a Route 53 Resolver DNS Firewall domain list resource.

## Basic Example

```yaml
resource:
  aws_route53_resolver_firewall_domain_list:
    example:
      name: example
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) A name that lets you identify the domain list, to manage and use it.
* `domains` - (Optional) A array of domains for the firewall domain list.
* `tags` - (Optional) A map of tags to assign to the resource. f configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN (Amazon Resource Name) of the domain list.
* `id` - The ID of the domain list.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_route53_resolver_firewall_domain_list.example rslvr-fdl-0123456789abcdef
```
