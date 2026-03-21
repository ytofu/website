# LB Listener

Manage LB Listener resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lb:
    front_end:

resource:
  aws_lb_target_group:
    front_end:

resource:
  aws_lb_listener:
    front_end:
      load_balancer_arn: ${aws_lb.front_end.arn}
      port: 443
      protocol: HTTPS
      ssl_policy: ELBSecurityPolicy-2016-08
      certificate_arn: "arn:aws:iam::187416307283:server-certificate/test_cert_rab3wuqwgja25ct3n4jdj2tzu4"
      default_action:
        type: forward
        target_group_arn: ${aws_lb_target_group.front_end.arn}
```

## Redirect Action

```yaml
resource:
  aws_lb:
    front_end:

resource:
  aws_lb_listener:
    front_end:
      load_balancer_arn: ${aws_lb.front_end.arn}
      port: 80
      protocol: HTTP
      default_action:
        type: redirect
        redirect:
          port: 443
          protocol: HTTPS
          status_code: HTTP_301
```

## Fixed-response Action

```yaml
resource:
  aws_lb:
    front_end:

resource:
  aws_lb_listener:
    front_end:
      load_balancer_arn: ${aws_lb.front_end.arn}
      port: 80
      protocol: HTTP
      default_action:
        type: fixed-response
        fixed_response:
          content_type: text/plain
          message_body: Fixed response content
          status_code: 200
```

## Authenticate-cognito Action

```yaml
resource:
  aws_lb:
    front_end:

resource:
  aws_lb_target_group:
    front_end:

resource:
  aws_cognito_user_pool:
    pool:

resource:
  aws_cognito_user_pool_client:
    client:

resource:
  aws_cognito_user_pool_domain:
    domain:

resource:
  aws_lb_listener:
    front_end:
      load_balancer_arn: ${aws_lb.front_end.arn}
      port: 80
      protocol: HTTP
      default_action:
        type: authenticate-cognito
        authenticate_cognito:
          user_pool_arn: ${aws_cognito_user_pool.pool.arn}
          user_pool_client_id: ${aws_cognito_user_pool_client.client.id}
          user_pool_domain: ${aws_cognito_user_pool_domain.domain.domain}
      default_action:
        type: forward
        target_group_arn: ${aws_lb_target_group.front_end.arn}
```

## Authenticate-OIDC Action

```yaml
resource:
  aws_lb:
    front_end:

resource:
  aws_lb_target_group:
    front_end:

resource:
  aws_lb_listener:
    front_end:
      load_balancer_arn: ${aws_lb.front_end.arn}
      port: 80
      protocol: HTTP
      default_action:
        type: authenticate-oidc
        authenticate_oidc:
          authorization_endpoint: "https://example.com/authorization_endpoint"
          client_id: client_id
          client_secret: client_secret
          issuer: "https://example.com"
          token_endpoint: "https://example.com/token_endpoint"
          user_info_endpoint: "https://example.com/user_info_endpoint"
      default_action:
        type: forward
        target_group_arn: ${aws_lb_target_group.front_end.arn}
```

## JWT Validation Action

```yaml
resource:
  aws_lb_listener:
    test:
      load_balancer_arn: ${aws_lb.test.id}
      protocol: HTTPS
      port: 443
      ssl_policy: ELBSecurityPolicy-2016-08
      certificate_arn: ${aws_iam_server_certificate.test.arn}
      default_action:
        type: jwt-validation
        jwt_validation:
          issuer: "https://example.com"
          jwks_endpoint: "https://example.com/.well-known/jwks.json"
          additional_claim:
            format: string-array
            name: claim_name1
            values: 
              - value1
              - value2
          additional_claim:
            format: single-string
            name: claim_name2
            values: 
              - value1
      default_action:
        target_group_arn: ${aws_lb_target_group.test.id}
        type: forward
```

## Gateway Load Balancer Listener

```yaml
resource:
  aws_lb:
    example:
      load_balancer_type: gateway
      name: example
      subnet_mapping:
        subnet_id: ${aws_subnet.example.id}

resource:
  aws_lb_target_group:
    example:
      name: example
      port: 6081
      protocol: GENEVE
      vpc_id: ${aws_vpc.example.id}
      health_check:
        port: 80
        protocol: HTTP

resource:
  aws_lb_listener:
    example:
      load_balancer_arn: ${aws_lb.example.id}
      default_action:
        target_group_arn: ${aws_lb_target_group.example.id}
        type: forward
```

## Mutual TLS Authentication

```yaml
resource:
  aws_lb:
    example:
      load_balancer_type: application

resource:
  aws_lb_target_group:
    example:

resource:
  aws_lb_listener:
    example:
      load_balancer_arn: ${aws_lb.example.id}
      default_action:
        target_group_arn: ${aws_lb_target_group.example.id}
        type: forward
      mutual_authentication:
        mode: verify
        trust_store_arn: ...
```
