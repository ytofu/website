# Resource: aws_lb_ssl_negotiation_policy

Provides a load balancer SSL negotiation policy, which allows an ELB to control the ciphers and protocols that are supported during SSL negotiations between a client and a load balancer.

## Basic Example

```yaml
resource:
  aws_elb:
    lb:
      name: test-lb
      availability_zones: 
        - us-east-1a
      listener:
        instance_port: 8000
        instance_protocol: https
        lb_port: 443
        lb_protocol: https
        ssl_certificate_id: "arn:aws:iam::123456789012:server-certificate/certName"

  aws_lb_ssl_negotiation_policy:
    foo:
      name: foo-policy
      load_balancer: ${aws_elb.lb.id}
      lb_port: 443
      attribute:
        name: Protocol-TLSv1
        value: false
      attribute:
        name: Protocol-TLSv1.1
        value: false
      attribute:
        name: Protocol-TLSv1.2
        value: true
      attribute:
        name: Server-Defined-Cipher-Order
        value: true
      attribute:
        name: ECDHE-RSA-AES128-GCM-SHA256
        value: true
      attribute:
        name: AES128-GCM-SHA256
        value: true
      attribute:
        name: EDH-RSA-DES-CBC3-SHA
        value: false```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the SSL negotiation policy.
* `load_balancer` - (Required) The load balancer to which the policy
  should be attached.
* `lb_port` - (Required) The load balancer port to which the policy
  should be applied. This must be an active listener on the load
balancer.
* `attribute` - (Optional) An SSL Negotiation policy attribute. Each has two properties:
    * `name` - The name of the attribute
    * `value` - The value of the attribute
* `triggers` - (Optional) Map of arbitrary keys and values that, when changed, will trigger a redeployment. To force a redeployment without changing these keys/values, use the `ytofu taint` command.

To set your attributes, please see the [AWS Elastic Load Balancing Developer Guide](http://docs.aws.amazon.com/ElasticLoadBalancing/latest/DeveloperGuide/elb-security-policy-table.html) for a listing of the supported SSL protocols, SSL options, and SSL ciphers.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the policy.
* `name` - The name of the stickiness policy.
* `load_balancer` - The load balancer to which the policy is attached.
* `lb_port` - The load balancer port to which the policy is applied.
* `attribute` - The SSL Negotiation policy attributes.
