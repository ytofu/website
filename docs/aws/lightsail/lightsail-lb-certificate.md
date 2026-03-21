# Resource: aws_lightsail_lb_certificate

Manages a Lightsail Load Balancer Certificate.

## Basic Example

```yaml
resource:
  aws_lightsail_lb:
    example:
      name: example-load-balancer
      health_check_path: /
      instance_port: 80
      tags:
        foo: bar

  aws_lightsail_lb_certificate:
    example:
      name: example-load-balancer-certificate
      lb_name: ${aws_lightsail_lb.example.id}
      domain_name: example.com```

## Argument Reference

The following arguments are required:

* `domain_name` - (Required) Domain name (e.g., example.com) for your SSL/TLS certificate.
* `lb_name` - (Required) Load balancer name where you want to create the SSL/TLS certificate.
* `name` - (Required) SSL/TLS certificate name.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `subject_alternative_names` - (Optional) Set of domains that should be SANs in the issued certificate. `domain_name` attribute is automatically added as a Subject Alternative Name.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the lightsail certificate.
* `created_at` - Timestamp when the instance was created.
* `domain_validation_records` - Set of domain validation objects which can be used to complete certificate validation. Can have more than one element, e.g., if SANs are defined.
* `id` - Combination of attributes to create a unique id: `lb_name`,`name`
* `support_code` - Support code for the certificate.

## Import

```bash
ytofu import aws_lightsail_lb_certificate.example example-load-balancer,example-load-balancer-certificate
```
