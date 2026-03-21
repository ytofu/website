# Resource: aws_swf_domain

Provides an SWF Domain resource.

## Basic Example

```yaml
resource:
  aws_swf_domain:
    foo:
      name: foo
      description: Terraform SWF Domain
      workflow_execution_retention_period_in_days: 30
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional, Forces new resource) The name of the domain. If omitted, ytofu will assign a random, unique name.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `description` - (Optional, Forces new resource) The domain description.
* `workflow_execution_retention_period_in_days` - (Required, Forces new resource) Length of time that SWF will continue to retain information about the workflow execution after the workflow execution is complete, must be between 0 and 90 days.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the domain.
* `arn` - Amazon Resource Name (ARN)
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_swf_domain.foo test-domain
```
