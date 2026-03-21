# Transcribe Vocabulary Filter

Manage Transcribe Vocabulary Filter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_transcribe_vocabulary_filter:
    example:
      vocabulary_filter_name: example
      language_code: en-US
      words: 
        - cars
        - bucket
      tags:
        tag1: value1
        tag2: value3
```
