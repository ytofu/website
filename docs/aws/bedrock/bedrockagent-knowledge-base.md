# Bedrockagent Knowledge Base

Manage Bedrockagent Knowledge Base resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagent_knowledge_base:
    example:
      name: example
      role_arn: ${aws_iam_role.example.arn}
      knowledge_base_configuration:
        vector_knowledge_base_configuration:
          embedding_model_arn: "arn:aws:bedrock:us-west-2::foundation-model/amazon.titan-embed-text-v2:0"
        type: VECTOR
      storage_configuration:
        type: OPENSEARCH_SERVERLESS
        opensearch_serverless_configuration:
          collection_arn: "arn:aws:aoss:us-west-2:123456789012:collection/142bezjddq707i5stcrf"
          vector_index_name: bedrock-knowledge-base-default-index
          field_mapping:
            vector_field: bedrock-knowledge-base-default-vector
            text_field: AMAZON_BEDROCK_TEXT_CHUNK
            metadata_field: AMAZON_BEDROCK_METADATA
```

## OpenSearch Managed Cluster Configuration

```yaml
resource:
  aws_bedrockagent_knowledge_base:
    example:
      name: example
      role_arn: ${aws_iam_role.example.arn}
      knowledge_base_configuration:
        vector_knowledge_base_configuration:
          embedding_model_arn: "arn:aws:bedrock:us-west-2::foundation-model/amazon.titan-embed-text-v2:0"
        type: VECTOR
      storage_configuration:
        type: OPENSEARCH_MANAGED_CLUSTER
        opensearch_managed_cluster_configuration:
          domain_arn: "arn:aws:es:us-west-2:123456789012:domain/example-domain"
          domain_endpoint: "https://search-example-domain.us-west-2.es.amazonaws.com"
          vector_index_name: example_index
          field_mapping:
            metadata_field: metadata
            text_field: chunks
            vector_field: embedding
```

## With Supplemental Data Storage Configuration

```yaml
resource:
  aws_bedrockagent_knowledge_base:
    example:
      name: example
      role_arn: ${aws_iam_role.example.arn}
      knowledge_base_configuration:
        vector_knowledge_base_configuration:
          embedding_model_arn: "arn:aws:bedrock:us-west-2::foundation-model/amazon.titan-embed-text-v2:0"
          embedding_model_configuration:
            bedrock_embedding_model_configuration:
              dimensions: 1024
              embedding_data_type: FLOAT32
          supplemental_data_storage_configuration:
            storage_location:
              type: S3
              s3_location:
                uri: "s3://my-bucket/chunk-processor/"
        type: VECTOR
      storage_configuration:
        type: OPENSEARCH_SERVERLESS
        opensearch_serverless_configuration:
          collection_arn: "arn:aws:aoss:us-west-2:123456789012:collection/142bezjddq707i5stcrf"
          vector_index_name: bedrock-knowledge-base-default-index
          field_mapping:
            vector_field: bedrock-knowledge-base-default-vector
            text_field: AMAZON_BEDROCK_TEXT_CHUNK
            metadata_field: AMAZON_BEDROCK_METADATA
```

## S3 Vectors Configuration

```yaml
resource:
  aws_s3vectors_vector_bucket:
    example:
      vector_bucket_name: example-bucket

resource:
  aws_s3vectors_index:
    example:
      index_name: example-index
      vector_bucket_name: ${aws_s3vectors_vector_bucket.example.vector_bucket_name}
      data_type: float32
      dimension: 256
      distance_metric: euclidean

resource:
  aws_bedrockagent_knowledge_base:
    example:
      name: example-s3vectors-kb
      role_arn: ${aws_iam_role.example.arn}
      knowledge_base_configuration:
        vector_knowledge_base_configuration:
          embedding_model_arn: "arn:aws:bedrock:us-west-2::foundation-model/amazon.titan-embed-text-v2:0"
          embedding_model_configuration:
            bedrock_embedding_model_configuration:
              dimensions: 256
              embedding_data_type: FLOAT32
        type: VECTOR
      storage_configuration:
        type: S3_VECTORS
        s3_vectors_configuration:
          index_arn: ${aws_s3vectors_index.example.index_arn}
```
