# ELB Attachment

Manage ELB Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_elb_attachment:
    baz:
      elb: ${aws_elb.bar.id}
      instance: ${aws_instance.foo.id}
```
