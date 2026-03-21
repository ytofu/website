# Resource: aws_pinpoint_apns_voip_channel

Provides a Pinpoint APNs VoIP Channel resource.

## Basic Example

```yaml
resource:
  aws_pinpoint_apns_voip_channel:
    apns_voip:
      application_id: ${aws_pinpoint_app.app.application_id}
      certificate: file-content
      private_key: file-content

  aws_pinpoint_app:
    app:```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `application_id` - (Required) The application ID.
* `enabled` - (Optional) Whether the channel is enabled or disabled. Defaults to `true`.
* `default_authentication_method` - (Optional) The default authentication method used for APNs.
  __NOTE__: Amazon Pinpoint uses this default for every APNs push notification that you send using the console.
  You can override the default when you send a message programmatically using the Amazon Pinpoint API, the AWS CLI, or an AWS SDK.
  If your default authentication type fails, Amazon Pinpoint doesn't attempt to use the other authentication type.

One of the following sets of credentials is also required.

If you choose to use __Certificate credentials__ you will have to provide:

* `certificate` - (Required) The pem encoded TLS Certificate from Apple.
* `private_key` - (Required) The Certificate Private Key file (ie. `.key` file).

If you choose to use __Key credentials__ you will have to provide:

* `bundle_id` - (Required) The ID assigned to your iOS app. To find this value, choose Certificates, IDs & Profiles, choose App IDs in the Identifiers section, and choose your app.
* `team_id` - (Required) The ID assigned to your Apple developer account team. This value is provided on the Membership page.
* `token_key` - (Required) The `.p8` file that you download from your Apple developer account when you create an authentication key.
* `token_key_id` - (Required) The ID assigned to your signing key. To find this value, choose Certificates, IDs & Profiles, and choose your key in the Keys section.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_pinpoint_apns_voip_channel.apns_voip application-id
```
