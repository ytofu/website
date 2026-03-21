# Resource: aws_lexv2models_bot_version

ytofu resource for managing an AWS Lex V2 Models Bot Version.

## Basic Example

```yaml
resource:
  aws_lexv2models_bot_version:
    test:
      bot_id: ${aws_lexv2models_bot.test.id}
      locale_specification:
        source_bot_version: DRAFT
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `bot_id` - (Required) Idientifier of the bot to create the version for.
* `locale_specification` - (Required) Specifies the locales that Amazon Lex adds to this version. You can choose the draft version or any other previously published version for each locale. When you specify a source version, the locale data is copied from the source version to the new version.
* `description` - (Optional) A description of the version. Use the description to help identify the version in lists.
* `sourceBotVersion` - (Required) The version of a bot used for a bot locale. Valid values: `DRAFT`, a numeric version.

The `locale_specification` attribute value is a map with one or more entries, each of which has a locale name as the key and an object with the following attribute as the value:

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `bot_version` - Version number assigned to the version.
* `id` - A comma-delimited string concatinating `bot_id` and `bot_version`.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_lexv2models_bot_version.example id-12345678,1
```
