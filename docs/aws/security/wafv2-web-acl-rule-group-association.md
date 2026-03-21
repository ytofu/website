# Wafv2 Web Acl Rule Group Association

Manage Wafv2 Web Acl Rule Group Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_wafv2_web_acl:
    example:
      name: example-web-acl
      scope: REGIONAL
      default_action:
        allow:
        visibility_config:
          cloudwatch_metrics_enabled: true
          metric_name: example-web-acl
          sampled_requests_enabled: true
        lifecycle:
          ignore_changes: 
            - rule

resource:
  aws_wafv2_web_acl_rule_group_association:
    example:
      rule_name: example-rule-group-rule
      priority: 100
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      rule_group_reference:
        arn: ${aws_wafv2_rule_group.example.arn}
```

## Managed Rule Group

```yaml
resource:
  aws_wafv2_web_acl_rule_group_association:
    example:
      rule_name: aws-common-rule-set
      priority: 50
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      managed_rule_group:
        name: AWSManagedRulesCommonRuleSet
        vendor_name: AWS
```

## Managed Rule Group With Version

```yaml
resource:
  aws_wafv2_web_acl_rule_group_association:
    example:
      rule_name: aws-common-rule-set-versioned
      priority: 60
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      managed_rule_group:
        name: AWSManagedRulesCommonRuleSet
        vendor_name: AWS
        version: Version_1.0
```

## Managed Rule Group With Rule Action Overrides

```yaml
resource:
  aws_wafv2_web_acl_rule_group_association:
    example:
      rule_name: aws-common-rule-set-with-overrides
      priority: 70
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      managed_rule_group:
        name: AWSManagedRulesCommonRuleSet
        vendor_name: AWS
        rule_action_override:
          name: GenericRFI_BODY
          action_to_use:
              custom_request_handling:
                insert_header:
                  name: X-RFI-Override
                  value: counted
        rule_action_override:
          name: SizeRestrictions_BODY
          action_to_use:
            captcha:
```

## Managed Rule Group With Managed Rule Group Configs

```yaml
resource:
  aws_wafv2_web_acl_rule_group_association:
    example:
      rule_name: acfp-ruleset-with-rule-config
      priority: 70
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      managed_rule_group:
        name: AWSManagedRulesACFPRuleSet
        vendor_name: AWS
        managed_rule_group_configs:
          aws_managed_rules_acfp_rule_set:
            creation_path: /creation
            registration_page_path: /registration
            request_inspection:
              email_field:
                identifier: /email
              password_field:
                identifier: /password
              phone_number_fields:
                identifiers: 
                  - /phone1
                  - /phone2
              address_fields:
                identifiers: 
                  - home
                  - work
              payload_type: JSON
              username_field:
                identifier: /username
      visibility_config:
        cloudwatch_metrics_enabled: true
        metric_name: friendly-metric-name
        sampled_requests_enabled: true
```

## Custom Rule Group With Override Action

```yaml
resource:
  aws_wafv2_web_acl_rule_group_association:
    example:
      rule_name: example-rule-group-rule
      priority: 100
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      override_action: count
      rule_group_reference:
        arn: ${aws_wafv2_rule_group.example.arn}
```

## Custom Rule Group With Rule Action Overrides

```yaml
resource:
  aws_wafv2_web_acl_rule_group_association:
    example:
      rule_name: example-rule-group-rule
      priority: 100
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      rule_group_reference:
        arn: ${aws_wafv2_rule_group.example.arn}
        rule_action_override:
          name: geo-block-rule
          action_to_use:
              custom_request_handling:
                insert_header:
                  name: X-Geo-Block-Override
                  value: counted
        rule_action_override:
          name: rate-limit-rule
          action_to_use:
            captcha:
              custom_request_handling:
                insert_header:
                  name: X-Rate-Limit-Override
                  value: captcha-required
```

## CloudFront Web ACL

```yaml
resource:
  aws_wafv2_web_acl_rule_group_association:
    example:
      rule_name: cloudfront-rule-group-rule
      priority: 50
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}
      rule_group_reference:
        arn: ${aws_wafv2_rule_group.example.arn}
```
