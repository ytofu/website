# Resource: aws_evidently_segment

Provides a CloudWatch Evidently Segment resource.

## Basic Example

```yaml
resource:
  aws_evidently_segment:
    example:
      name: example
      pattern: "{\"Price\":[{\"numeric\":[\">\",10,\"<=\",20]}]}"
      tags: 
```

## With JSON object in pattern

```yaml
resource:
  aws_evidently_segment:
    example:
      name: example
      pattern: |
        {
        "Price": [
        {
        "numeric": [">",10,"<=",20]
        }
        ]
        }
      tags: 
```

## With Description

```yaml
resource:
  aws_evidently_segment:
    example:
      name: example
      pattern: "{\"Price\":[{\"numeric\":[\">\",10,\"<=\",20]}]}"
      description: example
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional, Forces new resource) Specifies the description of the segment.
* `name` - (Required, Forces new resource) A name for the segment.
* `pattern` - (Required, Forces new resource) The pattern to use for the segment. For more information about pattern syntax, see [Segment rule pattern syntax](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch-Evidently-segments.html#CloudWatch-Evidently-segments-syntax.html).
* `tags` - (Optional) Tags to apply to the segment. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the segment.
* `created_time` - The date and time that the segment is created.
* `experiment_count` - The number of experiments that this segment is used in. This count includes all current experiments, not just those that are currently running.
* `id` - The ID has the same value as the ARN of the segment.
* `last_updated_time` - The date and time that this segment was most recently updated.
* `launch_count` - The number of launches that this segment is used in. This count includes all current launches, not just those that are currently running.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_evidently_segment.example arn:aws:evidently:us-west-2:123456789012:segment/example
```
