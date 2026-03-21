# Servicecatalog Provisioned Product

Manage Servicecatalog Provisioned Product resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_servicecatalog_provisioned_product:
    example:
      name: example
      product_name: Example product
      provisioning_artifact_name: Example version
      provisioning_parameters:
        key: foo
        value: bar
      tags:
        foo: bar
```
