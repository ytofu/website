# Pinpoint Email Template

Manage Pinpoint Email Template resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_pinpoint_email_template:
    test:
      template_name: testing
      email_template:
        subject: testing
        text_part: we are testing template text part
        header:
          name: testingname
          value: testingvalue
```
