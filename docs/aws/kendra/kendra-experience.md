# Kendra Experience

Manage Kendra Experience resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kendra_experience:
    example:
      index_id: ${aws_kendra_index.example.id}
      description: My Kendra Experience
      name: example
      role_arn: ${aws_iam_role.example.arn}
      configuration:
        content_source_configuration:
          direct_put_content: true
          faq_ids: 
            - ${aws_kendra_faq.example.faq_id}
        user_identity_configuration:
          identity_attribute_name: 12345ec453-1546651e-79c4-4554-91fa-00b43ccfa245
```
