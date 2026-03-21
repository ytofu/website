# Wafv2 Web Acl Rule

Manage Wafv2 Web Acl Rule resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_wafv2_web_acl:
    example:
      name: example
      scope: REGIONAL
      default_action:
        allow:
        visibility_config:
          cloudwatch_metrics_enabled: false
          metric_name: example
          sampled_requests_enabled: false
        lifecycle:
          ignore_changes: 
            - rule

resource:
  aws_wafv2_web_acl_rule:
    block_countries:
      name: "block-countries" # Must match existing rule name
      priority: 1
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      action:
        block:
        statement:
          geo_match_statement:
            country_codes: 
              - CN
              - RU
        visibility_config:
          cloudwatch_metrics_enabled: false
          metric_name: block-countries
          sampled_requests_enabled: false
```

## Basic Geo Match Rule

```yaml
resource:
  aws_wafv2_web_acl:
    example:
      name: example
      scope: REGIONAL
      default_action:
        allow:
        visibility_config:
          cloudwatch_metrics_enabled: false
          metric_name: example
          sampled_requests_enabled: false
        lifecycle:
          ignore_changes: 
            - rule

resource:
  aws_wafv2_web_acl_rule:
    block_countries:
      name: block-countries
      priority: 1
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      action:
        block:
        statement:
          geo_match_statement:
            country_codes: 
              - CN
              - RU
        visibility_config:
          cloudwatch_metrics_enabled: false
          metric_name: block-countries
          sampled_requests_enabled: false
```

## IP Set Reference (Solves Deletion Ordering)

```yaml
resource:
  aws_wafv2_ip_set:
    blocked_ips:
      name: blocked-ips
      scope: REGIONAL
      ip_address_version: IPV4
      addresses: 
        - 1.2.3.4/32
        - 5.6.7.8/32

resource:
  aws_wafv2_web_acl:
    example:
      name: example
      scope: REGIONAL
      default_action:
        allow:
        visibility_config:
          cloudwatch_metrics_enabled: true
          metric_name: example
          sampled_requests_enabled: true
        lifecycle:
          ignore_changes: 
            - rule

resource:
  aws_wafv2_web_acl_rule:
    block_ips:
      name: block-bad-ips
      priority: 1
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      action:
        block:
        statement:
          ip_set_reference_statement:
            arn: ${aws_wafv2_ip_set.blocked_ips.arn}
        visibility_config:
          cloudwatch_metrics_enabled: true
          metric_name: block-bad-ips
          sampled_requests_enabled: true
```

## Rate-Based Rule

```yaml
resource:
  aws_wafv2_web_acl_rule:
    rate_limit:
      name: rate-limit
      priority: 2
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      action:
        block:
        statement:
          rate_based_statement:
            limit: 2000
            aggregate_key_type: IP
        visibility_config:
          cloudwatch_metrics_enabled: true
          metric_name: rate-limit
          sampled_requests_enabled: true
```

## Managed Rule Group with Override Action

```yaml
resource:
  aws_wafv2_web_acl_rule:
    aws_managed_rules:
      name: aws-managed-rules
      priority: 3
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      override_action:
        none:
        statement:
          managed_rule_group_statement:
            name: AWSManagedRulesCommonRuleSet
            vendor_name: AWS
        visibility_config:
          cloudwatch_metrics_enabled: true
          metric_name: aws-managed-rules
          sampled_requests_enabled: true
```

## Custom Request Handling

```yaml
resource:
  aws_wafv2_web_acl_rule:
    captcha_with_headers:
      name: captcha-with-headers
      priority: 4
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      action:
        captcha:
          custom_request_handling:
            insert_header:
              name: x-captcha-rule
              value: triggered
      statement:
        geo_match_statement:
          country_codes: 
            - US
      visibility_config:
        cloudwatch_metrics_enabled: true
        metric_name: captcha-with-headers
        sampled_requests_enabled: true
```

## IP Set Reference

```yaml
resource:
  aws_wafv2_web_acl_rule:
    blocked_ips:
      name: blocked-ips
      priority: 1
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      action:
        block:
        statement:
          ip_set_reference_statement:
            arn: ${aws_wafv2_ip_set.blocked_ips.arn}
        visibility_config:
          cloudwatch_metrics_enabled: true
          metric_name: block-bad-ips
          sampled_requests_enabled: true
```

## Logical AND Statement

```yaml
resource:
  aws_wafv2_web_acl_rule:
    block_suspicious:
      name: block-suspicious
      priority: 1
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      action:
        block:
        statement:
          and_statement:
            statement:
              geo_match_statement:
                country_codes: 
                  - CN
            statement:
              byte_match_statement:
                search_string: admin
                positional_constraint: CONTAINS
                field_to_match:
                  uri_path:
                  text_transformation:
                    priority: 0
                    type: LOWERCASE
          visibility_config:
            cloudwatch_metrics_enabled: true
            metric_name: block-suspicious
            sampled_requests_enabled: true
```

## Logical OR Statement

```yaml
resource:
  aws_wafv2_web_acl_rule:
    block_countries:
      name: block-countries
      priority: 2
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      action:
        block:
        statement:
          or_statement:
            statement:
              geo_match_statement:
                country_codes: 
                  - CN
            statement:
              geo_match_statement:
                country_codes: 
                  - RU
        visibility_config:
          cloudwatch_metrics_enabled: true
          metric_name: block-countries
          sampled_requests_enabled: true
```

## Logical NOT Statement

```yaml
resource:
  aws_wafv2_web_acl_rule:
    allow_only_us:
      name: allow-only-us
      priority: 3
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      action:
        block:
        statement:
          not_statement:
            statement:
              geo_match_statement:
                country_codes: 
                  - US
                  - CA
        visibility_config:
          cloudwatch_metrics_enabled: true
          metric_name: allow-only-us
          sampled_requests_enabled: true
```
