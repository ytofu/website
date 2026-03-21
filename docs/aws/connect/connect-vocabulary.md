# Connect Vocabulary

Manage Connect Vocabulary resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_vocabulary:
    example:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: example
      content: Phrase\tIPA\tSoundsLike\tDisplayAs\nLos-Angeles\t\t\tLos Angeles\nF.B.I.\tɛ f b i aɪ\t\tFBI\nEtienne\t\teh-tee-en\t
      language_code: en-US
      tags: 
```
