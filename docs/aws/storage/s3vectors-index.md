# S3vectors Index

Manage S3vectors Index resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3vectors_index:
    example:
      index_name: example-index
      vector_bucket_name: ${aws_s3vectors_vector_bucket.example.vector_bucket_name}
      data_type: float32
      dimension: 2
      distance_metric: euclidean
```
