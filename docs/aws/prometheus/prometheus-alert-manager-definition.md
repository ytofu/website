# Resource: aws_prometheus_alert_manager_definition

Manages an Amazon Managed Service for Prometheus (AMP) Alert Manager Definition

## Basic Example

```yaml
resource:
  aws_prometheus_workspace:
    demo:

  aws_prometheus_alert_manager_definition:
    demo:
      workspace_id: ${aws_prometheus_workspace.demo.id}
      definition: |
        alertmanager_config: |
        route:
        receiver: 'default'
        receivers:
        - name: 'default'```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `workspace_id` - (Required) ID of the prometheus workspace the alert manager definition should be linked to
* `definition` - (Required) the alert manager definition that you want to be applied. See more [in AWS Docs](https://docs.aws.amazon.com/prometheus/latest/userguide/AMP-alert-manager.html).

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_prometheus_alert_manager_definition.demo ws-C6DCB907-F2D7-4D96-957B-66691F865D8B
```
