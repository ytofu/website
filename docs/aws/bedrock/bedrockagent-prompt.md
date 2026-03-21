# Bedrockagent Prompt

Manage Bedrockagent Prompt resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagent_prompt:
    example:
      name: MyPrompt
      description: My prompt description.
```

## With Variants

```yaml
resource:
  aws_bedrockagent_prompt:
    example:
      name: MakePlaylist
      description: My first prompt.
      default_variant: Variant1
      variant:
        name: Variant1
        model_id: amazon.titan-text-express-v1
        inference_configuration:
          text:
            temperature: 0.8
        template_type: TEXT
        template_configuration:
          text:
            text: "Make me a {{genre}} playlist consisting of the following number of songs: {{number}}."
            input_variable:
              name: genre
            input_variable:
              name: number
```
