# Imagebuilder Container Recipe

Manage Imagebuilder Container Recipe resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_imagebuilder_container_recipe:
    example:
      name: example
      version: 1.0.0
      container_type: DOCKER
      parent_image: "arn:aws:imagebuilder:eu-central-1:aws:image/amazon-linux-x86-latest/x.x.x"
      target_repository:
        repository_name: ${aws_ecr_repository.example.name}
        service: ECR
      component:
        component_arn: ${aws_imagebuilder_component.example.arn}
        parameter:
          name: Parameter1
          value: Value1
        parameter:
          name: Parameter2
          value: Value2
      dockerfile_template_data: |
        FROM {{{ imagebuilder:parentImage }}}
        {{{ imagebuilder:environments }}}
        {{{ imagebuilder:components }}}
```
