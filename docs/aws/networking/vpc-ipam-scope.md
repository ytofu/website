# Resource: aws_vpc_ipam_scope

Creates a scope for AWS IPAM.

## Basic Example

```yaml
data:
  aws_region:
    current:

resource:
  aws_vpc_ipam:
    example:
      operating_regions:
        region_name: ${data.aws_region.current.region}

resource:
  aws_vpc_ipam_scope:
    example:
      ipam_id: ${aws_vpc_ipam.example.id}
      description: Another Scope
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `ipam_id` - The ID of the IPAM for which you're creating this scope.
* `description` - (Optional) A description for the scope you're creating.
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of the scope.
* `id` - The ID of the IPAM Scope.
* `ipam_arn` - The ARN of the IPAM for which you're creating this scope.
* `is_default` - Defines if the scope is the default scope or not.
* `pool_count` - The number of pools in the scope.
* `type` - The type of the scope.

## Import

```bash
ytofu import aws_vpc_ipam_scope.example ipam-scope-0513c69f283d11dfb
```
