# IAM Openid Connect Provider

Manage IAM Openid Connect Provider resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_openid_connect_provider:
    default:
      url: "https://accounts.google.com"
      client_id_list:
        - 266362248691-342342xasdasdasda-apps.googleusercontent.com
      thumbprint_list: 
        - cf23df2207d99a74fbe169e3eba035e633b65d94
```

## Without A Thumbprint

```yaml
resource:
  aws_iam_openid_connect_provider:
    default:
      url: "https://accounts.google.com"
      client_id_list:
        - 266362248691-342342xasdasdasda-apps.googleusercontent.com
```
