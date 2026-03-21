# Resource: aws_ram_resource_share_accepter

Manage accepting a Resource Access Manager (RAM) Resource Share invitation. From a _receiver_ AWS account, accept an invitation to share resources that were shared by a _sender_ AWS account. To create a resource share in the _sender_, see the `aws_ram_resource_share` resource.

## Basic Example

```yaml
resource:
  aws_ram_resource_share:
    sender_share:
      name: tf-test-resource-share
      allow_external_principals: true
      tags:
        Name: tf-test-resource-share

  aws_ram_principal_association:
    sender_invite:
      principal: ${data.aws_caller_identity.receiver.account_id}
      resource_share_arn: ${aws_ram_resource_share.sender_share.arn}

  aws_ram_resource_share_accepter:
    receiver_accept:
      share_arn: ${aws_ram_principal_association.sender_invite.resource_share_arn}

data:
  aws_caller_identity:
    receiver:```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `share_arn` - (Required) The ARN of the resource share.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `invitation_arn` - The ARN of the resource share invitation.
* `share_id` - The ID of the resource share as displayed in the console.
* `status` - The status of the resource share (ACTIVE, PENDING, FAILED, DELETING, DELETED).
* `receiver_account_id` - The account ID of the receiver account which accepts the invitation.
* `sender_account_id` - The account ID of the sender account which submits the invitation.
* `share_name` - The name of the resource share.
* `resources` - A list of the resource ARNs shared via the resource share.

## Import

```bash
ytofu import aws_ram_resource_share_accepter.example arn:aws:ram:us-east-1:123456789012:resource-share/c4b56393-e8d9-89d9-6dc9-883752de4767
```
