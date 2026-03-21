# Rekognition Stream Processor

Manage Rekognition Stream Processor resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-bucket

resource:
  aws_sns_topic:
    example:
      name: example-topic

resource:
  aws_kinesis_video_stream:
    example:
      name: example-kinesis-input
      data_retention_in_hours: 1
      device_name: kinesis-video-device-name
      media_type: video/h264

resource:
  aws_iam_role:
    example:
      name: example-role
      inline_policy:
        name: Rekognition-Access
        policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["s3:PutObject"] "Effect": "Allow" "Resource": ["${aws_s3_bucket.example.arn}/*"] }, { "Action": ["sns:Publish"] "Effect": "Allow" "Resource": [aws_sns_topic.example.arn] }, { "Action": [ "kinesis:Get*", "kinesis:DescribeStreamSummary" ] "Effect": "Allow" "Resource": [aws_kinesis_video_stream.example.arn] }, ] }'
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "rekognition.amazonaws.com" } }, ] }'

resource:
  aws_rekognition_stream_processor:
    example:
      role_arn: ${aws_iam_role.example.arn}
      name: example-processor
      data_sharing_preference:
        opt_in: false
      output:
        s3_destination:
          bucket: ${aws_s3_bucket.example.bucket}
      settings:
        connected_home:
          labels: 
            - PERSON
            - PET
      input:
        kinesis_video_stream:
          arn: ${aws_kinesis_video_stream.example.arn}
      notification_channel:
        sns_topic_arn: ${aws_sns_topic.example.arn}
```

## Face Detection Usage

```yaml
resource:
  aws_kinesis_video_stream:
    example:
      name: example-kinesis-input
      data_retention_in_hours: 1
      device_name: kinesis-video-device-name
      media_type: video/h264

resource:
  aws_kinesis_stream:
    example:
      name: terraform-kinesis-example
      shard_count: 1

resource:
  aws_iam_role:
    example:
      name: example-role
      inline_policy:
        name: Rekognition-Access
        policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "kinesis:Get*", "kinesis:DescribeStreamSummary" ] "Effect": "Allow" "Resource": [aws_kinesis_video_stream.example.arn] }, { "Action": [ "kinesis:PutRecord" ] "Effect": "Allow" "Resource": [aws_kinesis_stream.example.arn] }, ] }'
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Principal": { "Service": "rekognition.amazonaws.com" } }, ] }'

resource:
  aws_rekognition_collection:
    example:
      collection_id: example-collection

resource:
  aws_rekognition_stream_processor:
    example:
      role_arn: ${aws_iam_role.example.arn}
      name: example-processor
      data_sharing_preference:
        opt_in: false
      regions_of_interest:
        polygon:
          x: 0.5
          y: 0.5
        polygon:
          x: 0.5
          y: 0.5
        polygon:
          x: 0.5
          y: 0.5
      input:
        kinesis_video_stream:
          arn: ${aws_kinesis_video_stream.example.arn}
      output:
        kinesis_data_stream:
          arn: ${aws_kinesis_stream.example.arn}
      settings:
        face_search:
          collection_id: ${aws_rekognition_collection.example.id}
```
