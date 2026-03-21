# Resource: aws_elastic_beanstalk_configuration_template

Provides an Elastic Beanstalk Configuration Template, which are associated with
a specific application and are used to deploy different versions of the
application with the same configuration settings.

## Basic Example

```yaml
resource:
  aws_elastic_beanstalk_configuration_template:
    example:
      name: tf-test-template-config
      application: ${aws_elastic_beanstalk_application.example.name}
      solution_stack_name: 64bit Amazon Linux 2015.09 v2.0.8 running Go 1.4

resource:
  aws_elastic_beanstalk_application:
    example:
      name: tf-test-name
      description: tf-test-desc
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) A unique name for this Template.
* `application` - (Required) name of the application to associate with this configuration template
* `description` - (Optional) Short description of the Template
* `environment_id` - (Optional) The ID of the environment used with this configuration template
* `setting` - (Optional) Option settings to configure the new Environment. These
  override specific values that are set as defaults. The format is detailed
  below in [Option Settings](#option-settings)
* `solution_stack_name` - (Optional) A solution stack to base your Template
off of. Example stacks can be found in the [Amazon API documentation][1]

## Attribute Reference

This resource exports no additional attributes.

[1]: https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts.platforms.html
