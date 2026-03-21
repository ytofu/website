# Resource: aws_appsync_domain_name_api_association

Provides an AppSync API Association.

## Basic Example

```yaml
resource:
  aws_appsync_domain_name_api_association:
    example:
      api_id: ${aws_appsync_graphql_api.example.id}
      domain_name: ${aws_appsync_domain_name.example.domain_name}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `api_id` - (Required) API ID.
* `domain_name` - (Required) Appsync domain name.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Appsync domain name.

## Import

```bash
ytofu import aws_appsync_domain_name_api_association.example example.com
```
