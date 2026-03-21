# Resource: aws_lightsail_domain

Manages a Lightsail domain for DNS management. Use this resource to manage DNS records for a domain that you have already registered with a domain registrar.

## Basic Example

```yaml
resource:
  aws_lightsail_domain:
    example:
      domain_name: example.com
```

## Argument Reference

The following arguments are required:

* `domain_name` - (Required) Name of the Lightsail domain to manage.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Lightsail domain.
* `id` - Name used for this domain.
