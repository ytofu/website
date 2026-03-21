# Resource: aws_medialive_multiplex_program

ytofu resource for managing an AWS MediaLive MultiplexProgram.

## Basic Example

```yaml
data:
  aws_availability_zones:
    available:
      state: available

resource:
  aws_medialive_multiplex:
    example:
      name: example-multiplex-changed
      availability_zones: 
        - ${data.aws_availability_zones.available.names[0]}
        - ${data.aws_availability_zones.available.names[1]}
      multiplex_settings:
        transport_stream_bitrate: 1000000
        transport_stream_id: 1
        transport_stream_reserved_bitrate: 1
        maximum_video_buffer_delay_milliseconds: 1000
      start_multiplex: true
      tags:
        tag1: value1

resource:
  aws_medialive_multiplex_program:
    example:
      program_name: example_program
      multiplex_id: ${aws_medialive_multiplex.example.id}
      multiplex_program_settings:
        program_number: 1
        preferred_channel_pipeline: CURRENTLY_ACTIVE
        video_settings:
          constant_bitrate: 100000
```

## Argument Reference

The following arguments are required:

* `multiplex_id` - (Required) Multiplex ID.
* `program_name` - (Required) Unique program name.
* `multiplex_program_settings` - (Required) MultiplexProgram settings. See [Multiplex Program Settings](#multiple-program-settings) for more details.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

### Multiple Program Settings

* `program_number` - (Required) Unique program number.
* `preferred_channel_pipeline` - (Required) Enum for preferred channel pipeline. Options are `CURRENTLY_ACTIVE`, `PIPELINE_0`, or `PIPELINE_1`.
* `service_descriptor` - (Optional) Service Descriptor. See [Service Descriptor](#service-descriptor) for more details.
* `video_settings` - (Optional) Video settings. See [Video Settings](#video-settings) for more details.

### Service Descriptor

* `provider_name` - (Required) Unique provider name.
* `service_name` - (Required) Unique service name.

### Video Settings

* `constant_bitrate` - (Optional) Constant bitrate value.
* `statmux_settings` - (Optional) Statmux settings. See [Statmux Settings](#statmux-settings) for more details.

### Statmux Settings

* `minimum_bitrate` - (Optional) Minimum bitrate.
* `maximum_bitrate` - (Optional) Maximum bitrate.
* `priority` - (Optional) Priority value.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the MultiplexProgram.
* `example_attribute` - Concise description.

## Timeouts

Configuration options:

- `create` - (Default `30s`)

## Import

```bash
ytofu import aws_medialive_multiplex_program.example example_program/1234567
```
