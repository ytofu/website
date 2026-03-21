# Resource: aws_servicequotas_service_quota

Manages an individual Service Quota.

## Basic Example

```yaml
resource:
  aws_servicequotas_service_quota:
    example:
      quota_code: L-F678F1CE
      service_code: vpc
      value: 75
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `quota_code` - (Required) Code of the service quota to track. For example: `L-F678F1CE`. Available values can be found with the [AWS CLI service-quotas list-service-quotas command](https://docs.aws.amazon.com/cli/latest/reference/service-quotas/list-service-quotas.html).
* `service_code` - (Required) Code of the service to track. For example: `vpc`. Available values can be found with the [AWS CLI service-quotas list-services command](https://docs.aws.amazon.com/cli/latest/reference/service-quotas/list-services.html).
* `value` - (Required) Float specifying the desired value for the service quota. If the desired value is higher than the current value, a quota increase request is submitted. When a known request is submitted and pending, the value reflects the desired value of the pending request.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `adjustable` - Whether the service quota can be increased.
* `arn` - Amazon Resource Name (ARN) of the service quota.
* `default_value` - Default value of the service quota.
* `id` - Service code and quota code, separated by a front slash (`/`)
* `quota_name` - Name of the quota.
* `service_name` - Name of the service.
* `usage_metric` - Information about the measurement.
    * `metric_dimensions` - The metric dimensions.
        * `class`
        * `resource`
        * `service`
        * `type`
    * `metric_name` - The name of the metric.
    * `metric_namespace` - The namespace of the metric.
    * `metric_statistic_recommendation` - The metric statistic that AWS recommend you use when determining quota usage.

## Import

```bash
ytofu import aws_servicequotas_service_quota.example vpc/L-F678F1CE
```
