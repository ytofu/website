# Resource: aws_devopsguru_event_sources_config

ytofu resource for managing an AWS DevOps Guru Event Sources Config. Currently the only service that can be integrated with DevOps Guru is Amazon CodeGuru Profiler, which can produce proactive recommendations which can be stored and viewed in DevOps Guru.

## Basic Example

```yaml
resource:
  aws_devopsguru_event_sources_config:
    example:
      event_sources:
        amazon_code_guru_profiler:
          status: ENABLED
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `event_sources` - (Required) Configuration information about the integration of DevOps Guru as the Consumer via EventBridge with another AWS Service. See [`event_sources`](#event_sources-argument-reference) below.

### `event_sources` Argument Reference

* `amazon_code_guru_profiler` - (Required) Stores whether DevOps Guru is configured to consume recommendations which are generated from AWS CodeGuru Profiler. See [`amazon_code_guru_profiler`](#amazon_code_guru_profiler-argument-reference) below.

### `amazon_code_guru_profiler` Argument Reference

* `status` - (Required) Status of the CodeGuru Profiler integration. Valid values are `ENABLED` and `DISABLED`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - AWS region.

## Import

```bash
ytofu import aws_devopsguru_event_sources_config.example us-east-1
```
