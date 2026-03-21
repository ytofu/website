# Resource: aws_servicequotas_template

ytofu resource for managing an AWS Service Quotas Template.

## Basic Example

```yaml
resource:
  aws_servicequotas_template:
    example:
      aws_region: us-east-1
      quota_code: "L-2ACBD22F" # function and layer storage (default: 75 GB)
      service_code: lambda
      value: 80
```

## Argument Reference

This resource supports the following arguments:

* `aws_region` - (Optional) AWS Region to which the template applies.
* `quota_code` - (Required) Quota identifier. To find the quota code for a specific quota, use the [aws_servicequotas_service_quota](../d/servicequotas_service_quota.html.markdown) data source.
* `service_code` - (Required) Service identifier. To find the service code value for an AWS service, use the [aws_servicequotas_service](../d/servicequotas_service.html.markdown) data source.
* `value` - (Required) The new, increased value for the quota.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `global_quota` - Indicates whether the quota is global.
* `id` - Unique identifier for the resource, which is a comma-delimited string separating `region`, `quota_code`, and `service_code`.
* `quota_name` - Quota name.
* `service_name` - Service name.
* `unit` - Unit of measurement.

## Import

```bash
ytofu import aws_servicequotas_template.example us-east-1,L-2ACBD22F,lambda
```
