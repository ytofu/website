# Resource: aws_lightsail_domain_entry

Manages a Lightsail domain entry (DNS record). Use this resource to define how DNS queries for your domain are handled.

## Basic Example

```yaml
resource:
  aws_lightsail_domain:
    example:
      domain_name: example.com

resource:
  aws_lightsail_domain_entry:
    example:
      domain_name: ${aws_lightsail_domain.example.domain_name}
      name: www
      type: A
      target: 127.0.0.1
```

## Argument Reference

The following arguments are required:

* `domain_name` - (Required) Name of the Lightsail domain in which to create the entry.
* `name` - (Required) Name of the entry record.
* `target` - (Required) Target of the domain entry.
* `type` - (Required) Type of record. Valid values: `A`, `AAAA`, `CNAME`, `MX`, `NS`, `SOA`, `SRV`, `TXT`.

The following arguments are optional:

* `is_alias` - (Optional) Whether the entry should be an alias. Default: `false`.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Combination of attributes to create a unique id: `name`,`domain_name`,`type`,`target`.

## Import

```bash
ytofu import aws_lightsail_domain_entry.example www,example.com,A,127.0.0.1
```
