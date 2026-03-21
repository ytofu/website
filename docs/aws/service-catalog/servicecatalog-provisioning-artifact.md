# Servicecatalog Provisioning Artifact

Manage Servicecatalog Provisioning Artifact resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_servicecatalog_provisioning_artifact:
    example:
      name: example
      product_id: ${aws_servicecatalog_product.example.id}
      type: CLOUD_FORMATION_TEMPLATE
      template_url: "https://${aws_s3_bucket.example.bucket_regional_domain_name}/${aws_s3_object.example.key}"
```
