# Lexv2models Intent

Manage Lexv2models Intent resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_partition:
    current:

resource:
  aws_iam_role:
    test:
      name: botens_namn
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "sts:AssumeRole" "Effect": "Allow" "Sid": "" "Principal": { "Service": "lexv2.amazonaws.com" } }, ] }'

resource:
  aws_iam_role_policy_attachment:
    test:
      role: ${aws_iam_role.test.name}
      policy_arn: "arn:${data.aws_partition.current.partition}:iam::aws:policy/AmazonLexFullAccess"

resource:
  aws_lexv2models_bot:
    test:
      name: botens_namn
      idle_session_ttl_in_seconds: 60
      role_arn: ${aws_iam_role.test.arn}
      data_privacy:
        child_directed: true

resource:
  aws_lexv2models_bot_locale:
    test:
      locale_id: en_US
      bot_id: ${aws_lexv2models_bot.test.id}
      bot_version: DRAFT
      n_lu_intent_confidence_threshold: 0.7

resource:
  aws_lexv2models_bot_version:
    test:
      bot_id: ${aws_lexv2models_bot.test.id}
      locale_specification:
        source_bot_version: DRAFT

resource:
  aws_lexv2models_intent:
    example:
      bot_id: ${aws_lexv2models_bot.test.id}
      bot_version: ${aws_lexv2models_bot_locale.test.bot_version}
      name: botens_namn
      locale_id: ${aws_lexv2models_bot_locale.test.locale_id}
```

## `confirmation_setting` Example

```yaml
resource:
  aws_lexv2models_intent:
    example:
      bot_id: ${aws_lexv2models_bot.test.id}
      bot_version: ${aws_lexv2models_bot_locale.test.bot_version}
      name: botens_namn
      locale_id: ${aws_lexv2models_bot_locale.test.locale_id}
      confirmation_setting:
        active: true
        prompt_specification:
          allow_interrupt: true
          max_retries: 1
          message_selection_strategy: Ordered
          prompt_attempts_specification:
            allow_interrupt: true
            map_block_key: Initial
            allowed_input_types:
              allow_audio_input: true
              allow_dtmf_input: true
            audio_and_dtmf_input_specification:
              start_timeout_ms: 4000
              audio_specification:
                end_timeout_ms: 640
                max_length_ms: 15000
              dtmf_specification:
                deletion_character: "*"
                end_character: "#"
                end_timeout_ms: 5000
                max_length: 513
            text_input_specification:
              start_timeout_ms: 30000
          prompt_attempts_specification:
            allow_interrupt: true
            map_block_key: Retry1
            allowed_input_types:
              allow_audio_input: true
              allow_dtmf_input: true
            audio_and_dtmf_input_specification:
              start_timeout_ms: 4000
              audio_specification:
                end_timeout_ms: 640
                max_length_ms: 15000
              dtmf_specification:
                deletion_character: "*"
                end_character: "#"
                end_timeout_ms: 5000
                max_length: 513
            text_input_specification:
              start_timeout_ms: 30000
```

## QnA Intent Example

```yaml
resource:
  aws_lexv2models_intent:
    qna_example:
      bot_id: ${aws_lexv2models_bot.test.id}
      bot_version: ${aws_lexv2models_bot_locale.test.bot_version}
      name: qna_intent
      locale_id: ${aws_lexv2models_bot_locale.test.locale_id}
      parent_intent_signature: AMAZON.QnAIntent
      qna_intent_configuration:
        data_source_configuration:
          kendra_configuration:
            kendra_index: ${aws_kendra_index.example.arn}
            exact_response: true
            query_filter_string_enabled: false
      sample_utterance:
        utterance: What is the answer?
```
