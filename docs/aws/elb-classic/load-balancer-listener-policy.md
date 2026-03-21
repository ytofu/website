# Resource: aws_load_balancer_listener_policy

Attaches a load balancer policy to an ELB Listener.

## Basic Example

```yaml
resource:
  aws_elb:
    wu-tang:
      name: wu-tang
      availability_zones: 
        - us-east-1a
      listener:
        instance_port: 443
        instance_protocol: http
        lb_port: 443
        lb_protocol: https
        ssl_certificate_id: "arn:aws:iam::000000000000:server-certificate/wu-tang.net"
      tags:
        Name: wu-tang

  aws_load_balancer_policy:
    wu-tang-ssl:
      load_balancer_name: ${aws_elb.wu-tang.name}
      policy_name: wu-tang-ssl
      policy_type_name: SSLNegotiationPolicyType
      policy_attribute:
        name: ECDHE-ECDSA-AES128-GCM-SHA256
        value: true
      policy_attribute:
        name: Protocol-TLSv1.2
        value: true

  aws_load_balancer_listener_policy:
    wu-tang-listener-policies-443:
      load_balancer_name: ${aws_elb.wu-tang.name}
      load_balancer_port: 443
      policy_names:
        - ${aws_load_balancer_policy.wu-tang-ssl.policy_name}```

## AWS Predefined Security Policy

```yaml
resource:
  aws_elb:
    wu-tang:
      name: wu-tang
      availability_zones: 
        - us-east-1a
      listener:
        instance_port: 443
        instance_protocol: http
        lb_port: 443
        lb_protocol: https
        ssl_certificate_id: "arn:aws:iam::000000000000:server-certificate/wu-tang.net"
      tags:
        Name: wu-tang

  aws_load_balancer_policy:
    wu-tang-ssl-tls-1-1:
      load_balancer_name: ${aws_elb.wu-tang.name}
      policy_name: wu-tang-ssl
      policy_type_name: SSLNegotiationPolicyType
      policy_attribute:
        name: Reference-Security-Policy
        value: ELBSecurityPolicy-TLS-1-1-2017-01

  aws_load_balancer_listener_policy:
    wu-tang-listener-policies-443:
      load_balancer_name: ${aws_elb.wu-tang.name}
      load_balancer_port: 443
      policy_names:
        - ${aws_load_balancer_policy.wu-tang-ssl-tls-1-1.policy_name}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `load_balancer_name` - (Required) The load balancer to attach the policy to.
* `load_balancer_port` - (Required) The load balancer listener port to apply the policy to.
* `policy_names` - (Required) List of Policy Names to apply to the backend server.
* `triggers` - (Optional) Map of arbitrary keys and values that, when changed, will trigger an update. To force an update without changing these keys/values, use the `ytofu taint` command.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the policy.
* `load_balancer_name` - The load balancer on which the policy is defined.
* `load_balancer_port` - The load balancer listener port the policies are applied to
