# Resource: aws_elastic_beanstalk_application_version

Provides an Elastic Beanstalk Application Version Resource. Elastic Beanstalk allows
you to deploy and manage applications in the AWS cloud without worrying about
the infrastructure that runs those applications.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    default:
      bucket: tftest.applicationversion.bucket

  aws_s3_object:
    default:
      bucket: ${aws_s3_bucket.default.id}
      key: beanstalk/go-v1.zip
      source: go-v1.zip

  aws_elastic_beanstalk_application:
    default:
      name: tf-test-name
      description: tf-test-desc

  aws_elastic_beanstalk_application_version:
    default:
      name: tf-test-version-label
      application: tf-test-name
      description: application version created by terraform
      bucket: ${aws_s3_bucket.default.id}
      key: ${aws_s3_object.default.key}```

## Argument Reference

The following arguments are required:

* `application` - (Required) Name of the Beanstalk Application the version is associated with.
* `bucket` - (Required) S3 bucket that contains the Application Version source bundle.
* `key` - (Required) S3 object that is the Application Version source bundle.
* `name` - (Required) Unique name for the this Application Version.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` - (Optional) Short description of the Application Version.
* `force_delete` - (Optional) On delete, force an Application Version to be deleted when it may be in use by multiple Elastic Beanstalk Environments.
* `process` - (Optional) Pre-processes and validates the environment manifest (env.yaml ) and configuration files (*.config files in the .ebextensions folder) in the source bundle. Validating configuration files can identify issues prior to deploying the application version to an environment. You must turn processing on for application versions that you create using AWS CodeBuild or AWS CodeCommit. For application versions built from a source bundle in Amazon S3, processing is optional. It validates Elastic Beanstalk configuration files. It doesn’t validate your application’s configuration files, like proxy server or Docker configuration.
* `tags` - (Optional) Key-value map of tags for the Elastic Beanstalk Application Version. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN assigned by AWS for this Elastic Beanstalk Application.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
