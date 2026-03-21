# Bedrockagent Flow

Manage Bedrockagent Flow resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_bedrockagent_flow:
    example:
      name: example
      execution_role_arn: ${aws_iam_role.example.arn}
      definition:
        connection:
          name: FlowInputNodeFlowInputNode0ToPrompt_1PromptsNode0
          source: FlowInputNode
          target: Prompt_1
          type: Data
          configuration:
            data:
              source_output: document
              target_input: topic
        connection:
          name: Prompt_1PromptsNode0ToFlowOutputNodeFlowOutputNode0
          source: Prompt_1
          target: FlowOutputNode
          type: Data
          configuration:
            data:
              source_output: modelCompletion
              target_input: document
        node:
          name: FlowInputNode
          type: Input
          configuration:
            input:
            output:
              name: document
              type: String
          node:
            name: Prompt_1
            type: Prompt
            configuration:
              prompt:
                source_configuration:
                  inline:
                    model_id: amazon.titan-text-express-v1
                    template_type: TEXT
                    inference_configuration:
                      text:
                        max_tokens: 2048
                        stop_sequences: 
                          - "User:"
                        temperature: 0
                        top_p: 0.8999999761581421
                    template_configuration:
                      text:
                        text: "Write a paragraph about {{topic}}."
                        input_variable:
                          name: topic
            input:
              expression: $.data
              name: topic
              type: String
            output:
              name: modelCompletion
              type: String
          node:
            name: FlowOutputNode
            type: Output
            configuration:
              output:
              input:
                expression: $.data
                name: document
                type: String
```
