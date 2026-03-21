# Sagemaker Project

Manage Sagemaker Project resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_project:
    example:
      project_name: example
      service_catalog_provisioning_details:
        product_id: ${aws_servicecatalog_product.example.id}
```
