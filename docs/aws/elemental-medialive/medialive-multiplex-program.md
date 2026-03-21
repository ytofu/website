# Medialive Multiplex Program

Manage Medialive Multiplex Program resources using ytofu YAML.

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
