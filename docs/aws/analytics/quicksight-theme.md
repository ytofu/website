# Quicksight Theme

Manage Quicksight Theme resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_theme:
    example:
      theme_id: example
      name: example
      base_theme_id: MIDNIGHT
      configuration:
        data_color_palette:
          colors:
            - "#FFFFFF"
            - "#111111"
            - "#222222"
            - "#333333"
            - "#444444"
            - "#555555"
            - "#666666"
            - "#777777"
            - "#888888"
            - "#999999"
          empty_fill_color: "#FFFFFF"
          min_max_gradient:
            - "#FFFFFF"
            - "#111111"
```
