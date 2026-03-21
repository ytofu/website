# LB Trust Store

Manage LB Trust Store resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lb_trust_store:
    test:
      name: tf-example-lb-ts
      ca_certificates_bundle_s3_bucket: ...
      ca_certificates_bundle_s3_key: ...

resource:
  aws_lb_listener:
    example:
      load_balancer_arn: ${aws_lb.example.id}
      default_action:
        target_group_arn: ${aws_lb_target_group.example.id}
        type: forward
      mutual_authentication:
        mode: verify
        trust_store_arn: ${aws_lb_trust_store.test.arn}
```
