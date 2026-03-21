# Bedrockagent Data Source

Manage Bedrockagent Data Source resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagent_data_source:
    example:
      knowledge_base_id: EMDPPAYPZI
      name: example
      data_source_configuration:
        type: S3
        s3_configuration:
          bucket_arn: "arn:aws:s3:::example-bucket"
```

## Multimodal Parsing

```yaml
resource:
  aws_bedrockagent_data_source:
    example:
      knowledge_base_id: ${aws_bedrockagent_knowledge_base.example.id}
      name: multimodal-example
      data_source_configuration:
        type: S3
        s3_configuration:
          bucket_arn: ${aws_s3_bucket.example.arn}
      vector_ingestion_configuration:
        chunking_configuration:
          chunking_strategy: FIXED_SIZE
          fixed_size_chunking_configuration:
            max_tokens: 512
            overlap_percentage: 20
        parsing_configuration:
          parsing_strategy: BEDROCK_FOUNDATION_MODEL
          bedrock_foundation_model_configuration:
            model_arn: "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-3-sonnet-20240229-v1:0"
            parsing_modality: MULTIMODAL
            parsing_prompt:
              parsing_prompt_string: Extract and transcribe all text and visual content from the document.
```
