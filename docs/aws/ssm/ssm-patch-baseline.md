# SSM Patch Baseline

Manage SSM Patch Baseline resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssm_patch_baseline:
    production:
      name: patch-baseline
      approved_patches: 
        - KB123456
```

## Advanced Usage, specifying patch filters

```yaml
resource:
  aws_ssm_patch_baseline:
    production:
      name: patch-baseline
      description: Patch Baseline Description
      approved_patches: 
        - KB123456
        - KB456789
      rejected_patches: 
        - KB987654
      global_filter:
        key: PRODUCT
        values: 
          - WindowsServer2008
      global_filter:
        key: CLASSIFICATION
        values: 
          - ServicePacks
      global_filter:
        key: MSRC_SEVERITY
        values: 
          - Low
      approval_rule:
        approve_after_days: 7
        compliance_level: HIGH
        patch_filter:
          key: PRODUCT
          values: 
            - WindowsServer2016
        patch_filter:
          key: CLASSIFICATION
          values: 
            - CriticalUpdates
            - SecurityUpdates
            - Updates
        patch_filter:
          key: MSRC_SEVERITY
          values: 
            - Critical
            - Important
            - Moderate
      approval_rule:
        approve_after_days: 7
        patch_filter:
          key: PRODUCT
          values: 
            - WindowsServer2012
```

## Advanced usage, specifying Microsoft application and Windows patch rules

```yaml
resource:
  aws_ssm_patch_baseline:
    windows_os_apps:
      name: WindowsOSAndMicrosoftApps
      description: Patch both Windows and Microsoft apps
      operating_system: WINDOWS
      approval_rule:
        approve_after_days: 7
        patch_filter:
          key: CLASSIFICATION
          values: 
            - CriticalUpdates
            - SecurityUpdates
        patch_filter:
          key: MSRC_SEVERITY
          values: 
            - Critical
            - Important
      approval_rule:
        approve_after_days: 7
        patch_filter:
          key: PATCH_SET
          values: 
            - APPLICATION
        patch_filter:
          key: PRODUCT
          values: 
            - Office 2013
            - Office 2016
```

## Advanced usage, specifying alternate patch source repository

```yaml
resource:
  aws_ssm_patch_baseline:
    al_2017_09:
      name: Amazon-Linux-2017.09
      description: My patch repository for Amazon Linux 2017.09
      operating_system: AMAZON_LINUX
      approval_rule:
      source:
        name: My-AL2017.09
        products: 
          - AmazonLinux2017.09
        configuration: |
          [amzn-main]
          name=amzn-main-Base
          mirrorlist=http://repo./$awsregion./$awsdomain//$releasever/main/mirror.list
          mirrorlist_expire=300
          metadata_expire=300
          priority=10
          failovermethod=priority
          fastestmirror_enabled=0
          gpgcheck=1
          gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-amazon-ga
          enabled=1
          retries=3
          timeout=5
          report_instanceid=yes
```
