# Medialive Channel

Manage Medialive Channel resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_medialive_channel:
    example:
      name: example-channel
      channel_class: STANDARD
      role_arn: ${aws_iam_role.example.arn}
      input_specification:
        codec: AVC
        input_resolution: HD
        maximum_bitrate: MAX_20_MBPS
      input_attachments:
        input_attachment_name: example-input
        input_id: ${aws_medialive_input.example.id}
      destinations:
        id: destination
        settings:
          url: "s3://${aws_s3_bucket.main.id}/test1"
        settings:
          url: "s3://${aws_s3_bucket.main2.id}/test2"
      encoder_settings:
        timecode_config:
          source: EMBEDDED
        audio_descriptions:
          audio_selector_name: example audio selector
          name: audio-selector
        video_descriptions:
          name: example-video
        output_groups:
          output_group_settings:
            archive_group_settings:
              destination:
                destination_ref_id: destination
          outputs:
            output_name: example-name
            video_description_name: example-video
            audio_description_names: 
              - audio-selector
            output_settings:
              archive_output_settings:
                name_modifier: _1
                extension: m2ts
                container_settings:
                  m2ts_settings:
                    audio_buffer_model: ATSC
                    buffer_model: MULTIPLEX
                    rate_mode: CBR
```
