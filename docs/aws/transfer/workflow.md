# Transfer Workflow

Create file processing workflows using ytofu YAML.

## Copy and Tag Workflow

```yaml
resource:
  aws_transfer_workflow:
    example:
      steps:
        - copy_step_details:
            name: copy-to-archive
            destination_file_location:
              s3_file_location:
                bucket: ${aws_s3_bucket.archive.id}
                key: archive/
          type: COPY
        - tag_step_details:
            name: tag-file
            tags:
              - key: status
                value: processed
          type: TAG
```
