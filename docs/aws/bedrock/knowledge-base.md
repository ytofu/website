# Bedrock Knowledge Base

Create knowledge bases for Bedrock agents using ytofu YAML.

## OpenSearch Serverless Knowledge Base

```yaml
resource:
  aws_bedrockagent_knowledge_base:
    example:
      name: example
      role_arn: ${aws_iam_role.bedrock.arn}
      knowledge_base_configuration:
        vector_knowledge_base_configuration:
          embedding_model_arn: arn:aws:bedrock:us-east-1::foundation-model/amazon.titan-embed-text-v1
        type: VECTOR
      storage_configuration:
        type: OPENSEARCH_SERVERLESS
        opensearch_serverless_configuration:
          collection_arn: ${aws_opensearchserverless_collection.example.arn}
          vector_index_name: bedrock-index
          field_mapping:
            vector_field: vector
            text_field: text
            metadata_field: metadata
```

## S3 Data Source

```yaml
resource:
  aws_bedrockagent_data_source:
    example:
      knowledge_base_id: ${aws_bedrockagent_knowledge_base.example.id}
      name: example
      data_source_configuration:
        type: S3
        s3_configuration:
          bucket_arn: ${aws_s3_bucket.knowledge.arn}
```
