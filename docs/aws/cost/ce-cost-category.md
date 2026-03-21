# Ce Cost Category

Manage Ce Cost Category resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ce_cost_category:
    test:
      name: NAME
      rule_version: CostCategoryExpression.v1
      rule:
        value: production
        rule:
          dimension:
            key: LINKED_ACCOUNT_NAME
            values: 
              - -prod
            match_options: 
              - ENDS_WITH
      rule:
        value: staging
        rule:
          dimension:
            key: LINKED_ACCOUNT_NAME
            values: 
              - -stg
            match_options: 
              - ENDS_WITH
      rule:
        value: testing
        rule:
          dimension:
            key: LINKED_ACCOUNT_NAME
            values: 
              - -dev
            match_options: 
              - ENDS_WITH
```
