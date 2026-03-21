# Quicksight User

Manage Quicksight User resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_user:
    example:
      email: author1@example.com
      identity_type: IAM
      user_role: AUTHOR
      iam_arn: "arn:aws:iam::123456789012:role/AuthorRole"
      session_name: author1
```

## Create User With IAM Identity Type Using an IAM User

```yaml
resource:
  aws_quicksight_user:
    example:
      email: authorpro1@example.com
      identity_type: IAM
      user_role: AUTHOR_PRO
      iam_arn: "arn:aws:iam::123456789012:user/authorpro1"
```

## Create User With QuickSight Identity Type in Non-Default Namespace

```yaml
resource:
  aws_quicksight_user:
    example:
      email: reader1@example.com
      identity_type: QUICKSIGHT
      user_role: READER
      namespace: example
      user_name: reader1
```
