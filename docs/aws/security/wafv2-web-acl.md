# Wafv2 Web Acl

Manage Wafv2 Web Acl resources using ytofu YAML.

## Managed Rule

```yaml
resource:
  aws_wafv2_web_acl:
    example:
      name: managed-rule-example
      description: Example of a managed rule.
      scope: REGIONAL
      default_action:
        allow:
        rule:
          name: rule-1
          priority: 1
          override_action:
            statement:
              managed_rule_group_statement:
                name: AWSManagedRulesCommonRuleSet
                vendor_name: AWS
                rule_action_override:
                  action_to_use:
                    name: SizeRestrictions_QUERYSTRING
                  rule_action_override:
                    action_to_use:
                      name: NoUserAgent_HEADER
                    scope_down_statement:
                      geo_match_statement:
                        country_codes: 
                          - US
                          - NL
                visibility_config:
                  cloudwatch_metrics_enabled: false
                  metric_name: friendly-rule-metric-name
                  sampled_requests_enabled: false
              tags:
                Tag1: Value1
                Tag2: Value2
              token_domains: 
                - mywebsite.com
                - myotherwebsite.com
              visibility_config:
                cloudwatch_metrics_enabled: false
                metric_name: friendly-metric-name
                sampled_requests_enabled: false
```

## Account Creation Fraud Prevention

```yaml
resource:
  aws_wafv2_web_acl:
    acfp-example:
      name: managed-acfp-example
      description: Example of a managed ACFP rule.
      scope: CLOUDFRONT
      default_action:
        allow:
        rule:
          name: acfp-rule-1
          priority: 1
          override_action:
            statement:
              managed_rule_group_statement:
                name: AWSManagedRulesACFPRuleSet
                vendor_name: AWS
                managed_rule_group_configs:
                  aws_managed_rules_acfp_rule_set:
                    creation_path: /signin
                    registration_page_path: /register
                    request_inspection:
                      email_field:
                        identifier: /email
                      password_field:
                        identifier: /password
                      payload_type: JSON
                      username_field:
                        identifier: /username
                    response_inspection:
                      status_code:
                        failure_codes: 
                          - 403
                        success_codes: 
                          - 200
            visibility_config:
              cloudwatch_metrics_enabled: false
              metric_name: friendly-rule-metric-name
              sampled_requests_enabled: false
          visibility_config:
            cloudwatch_metrics_enabled: false
            metric_name: friendly-metric-name
            sampled_requests_enabled: false
```

## Account Takeover Protection

```yaml
resource:
  aws_wafv2_web_acl:
    atp-example:
      name: managed-atp-example
      description: Example of a managed ATP rule.
      scope: CLOUDFRONT
      default_action:
        allow:
        rule:
          name: atp-rule-1
          priority: 1
          override_action:
            statement:
              managed_rule_group_statement:
                name: AWSManagedRulesATPRuleSet
                vendor_name: AWS
                managed_rule_group_configs:
                  aws_managed_rules_atp_rule_set:
                    login_path: /api/1/signin
                    request_inspection:
                      password_field:
                        identifier: /password
                      payload_type: JSON
                      username_field:
                        identifier: /email
                    response_inspection:
                      status_code:
                        failure_codes: 
                          - 403
                        success_codes: 
                          - 200
            visibility_config:
              cloudwatch_metrics_enabled: false
              metric_name: friendly-rule-metric-name
              sampled_requests_enabled: false
          visibility_config:
            cloudwatch_metrics_enabled: false
            metric_name: friendly-metric-name
            sampled_requests_enabled: false
```

## Rate Based

```yaml
resource:
  aws_wafv2_web_acl:
    example:
      name: rate-based-example
      description: Example of a Cloudfront rate based statement.
      scope: CLOUDFRONT
      default_action:
        allow:
        rule:
          name: rule-1
          priority: 1
          action:
            block:
            statement:
              rate_based_statement:
                limit: 10000
                aggregate_key_type: IP
                scope_down_statement:
                  geo_match_statement:
                    country_codes: 
                      - US
                      - NL
            visibility_config:
              cloudwatch_metrics_enabled: false
              metric_name: friendly-rule-metric-name
              sampled_requests_enabled: false
          tags:
            Tag1: Value1
            Tag2: Value2
          visibility_config:
            cloudwatch_metrics_enabled: false
            metric_name: friendly-metric-name
            sampled_requests_enabled: false
```

## Rule Group Reference

```yaml
resource:
  aws_wafv2_rule_group:
    example:
      capacity: 10
      name: example-rule-group
      scope: REGIONAL
      rule:
        name: rule-1
        priority: 1
        action:
          statement:
            geo_match_statement:
              country_codes: 
                - NL
          visibility_config:
            cloudwatch_metrics_enabled: false
            metric_name: friendly-rule-metric-name
            sampled_requests_enabled: false
        rule:
          name: rule-to-exclude-a
          priority: 10
          action:
            allow:
            statement:
              geo_match_statement:
                country_codes: 
                  - US
            visibility_config:
              cloudwatch_metrics_enabled: false
              metric_name: friendly-rule-metric-name
              sampled_requests_enabled: false
          rule:
            name: rule-to-exclude-b
            priority: 15
            action:
              allow:
              statement:
                geo_match_statement:
                  country_codes: 
                    - GB
              visibility_config:
                cloudwatch_metrics_enabled: false
                metric_name: friendly-rule-metric-name
                sampled_requests_enabled: false
            visibility_config:
              cloudwatch_metrics_enabled: false
              metric_name: friendly-metric-name
              sampled_requests_enabled: false

resource:
  aws_wafv2_web_acl:
    test:
      name: rule-group-example
      scope: REGIONAL
      default_action:
        block:
        rule:
          name: rule-1
          priority: 1
          override_action:
            statement:
              rule_group_reference_statement:
                arn: ${aws_wafv2_rule_group.example.arn}
                rule_action_override:
                  action_to_use:
                    name: rule-to-exclude-b
                  rule_action_override:
                    action_to_use:
                      name: rule-to-exclude-a
                visibility_config:
                  cloudwatch_metrics_enabled: false
                  metric_name: friendly-rule-metric-name
                  sampled_requests_enabled: false
              tags:
                Tag1: Value1
                Tag2: Value2
              visibility_config:
                cloudwatch_metrics_enabled: false
                metric_name: friendly-metric-name
                sampled_requests_enabled: false
```

## Large Request Body Inspections for Regional Resources

```yaml
resource:
  aws_wafv2_web_acl:
    example:
      name: large-request-body-example
      scope: REGIONAL
      default_action:
        allow:
        association_config:
          request_body:
            api_gateway:
              default_size_inspection_limit: KB_64
            app_runner_service:
              default_size_inspection_limit: KB_64
            cognito_user_pool:
              default_size_inspection_limit: KB_64
            verified_access_instance:
              default_size_inspection_limit: KB_64
        visibility_config:
          cloudwatch_metrics_enabled: false
          metric_name: friendly-metric-name
          sampled_requests_enabled: false
```
