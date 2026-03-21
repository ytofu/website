# Resource: aws_ec2_traffic_mirror_filter

Provides an Traffic mirror filter.  
Read [limits and considerations](https://docs.aws.amazon.com/vpc/latest/mirroring/traffic-mirroring-considerations.html) for traffic mirroring

## Basic Example

```yaml
resource:
  aws_ec2_traffic_mirror_filter:
    foo:
      description: traffic mirror filter - terraform example
      network_services: 
        - amazon-dns
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional, Forces new resource) A description of the filter.
* `network_services` - (Optional) List of amazon network services that should be mirrored. Valid values: `amazon-dns`.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the traffic mirror filter.
* `id` - The name of the filter.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_ec2_traffic_mirror_filter.foo tmf-0fbb93ddf38198f64
```
