# IOT Provisioning Template

Manage IOT Provisioning Template resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    iot_assume_role_policy:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - iot.amazonaws.com

resource:
  aws_iam_role:
    iot_fleet_provisioning:
      name: IoTProvisioningServiceRole
      path: /service-role/
      assume_role_policy: ${data.aws_iam_policy_document.iot_assume_role_policy.json}

resource:
  aws_iam_role_policy_attachment:
    iot_fleet_provisioning_registration:
      role: ${aws_iam_role.iot_fleet_provisioning.name}
      policy_arn: "arn:aws:iam::aws:policy/service-role/AWSIoTThingsRegistration"

data:
  aws_iam_policy_document:
    device_policy:
      statement:
        actions: 
          - "iot:Subscribe"
        resources: 
          - "*"

resource:
  aws_iot_policy:
    device_policy:
      name: DevicePolicy
      policy: ${data.aws_iam_policy_document.device_policy.json}

resource:
  aws_iot_provisioning_template:
    fleet:
      name: FleetTemplate
      description: My provisioning template
      provisioning_role_arn: ${aws_iam_role.iot_fleet_provisioning.arn}
      enabled: true
      template_body: '{ "Parameters": { "SerialNumber": { "Type": "String" } } "Resources": { "certificate": { "Properties": { "CertificateId": { "Ref": "AWS::IoT::Certificate::Id" } "Status": "Active" } "Type": "AWS::IoT::Certificate" } "policy": { "Properties": { "PolicyName": aws_iot_policy.device_policy.name } "Type": "AWS::IoT::Policy" } } }'
```
