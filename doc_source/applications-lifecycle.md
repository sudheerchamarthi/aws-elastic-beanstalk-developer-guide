# Configuring Application Version Lifecycle Settings<a name="applications-lifecycle"></a>

Each time you upload a new version of your application with the Elastic Beanstalk console or the EB CLI, Elastic Beanstalk creates an [application version](applications-versions.md)\. If you don't delete versions that you no longer use, you will eventually reach the [application version limit](http://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html#limits_elastic_beanstalk) and be unable to create new versions of that application\.

You can avoid hitting the limit by applying an *application version lifecycle policy* to your applications\. A lifecycle policy tells Elastic Beanstalk to delete application versions that are old, or to delete application versions when the total number of versions for an application exceeds a specified number\.

Elastic Beanstalk applies an application's lifecycle policy each time you create a new application version, and deletes up to 100 versions each time the lifecycle policy is applied\. Elastic Beanstalk deletes old versions before creating the new version, and does not count the new version towards the maximum number of versions defined in the policy\.

Elastic Beanstalk does not delete application versions that are currently being used by an environment, or application versions deployed to environments that were terminated less than ten weeks before the policy was triggered\.

The application version limit applies across all applications in a region\. If you have several applications, configure each application with a lifecycle policy appropriate to avoid reaching the limit\. Elastic Beanstalk only applies the policy if the application version creation succeeds, so if you have already reached the limit, you must delete some versions manually prior to creating a new version\.

By default, Elastic Beanstalk leaves the application version's [source bundle](applications-sourcebundle.md) in Amazon S3 to prevent loss of data\. You can delete the source bundle to save space\.

You can set the lifecycle settings through the Elastic Beanstalk CLI and APIs\. See [`eb appversion`](eb3-appversion.md), [CreateApplication](http://docs.aws.amazon.com/elasticbeanstalk/latest/api/API_CreateApplication.html) \(using the `ResourceLifecycleConfig` parameter\), and [UpdateApplicationResourceLifecycle](http://docs.aws.amazon.com/elasticbeanstalk/latest/api/API_UpdateApplicationResourceLifecycle.html) for details\.

## Setting the Application Lifecycle Settings in the Console<a name="applications-lifecycle-console"></a>

You can specify the lifecycle settings in the console\.

**To specify your application lifecycle settings\.**

1. Open the [Elastic Beanstalk console](https://console.aws.amazon.com/elasticbeanstalk)\.

1. Choose an application\.

1. In the navigation pane, select **Application versions**\.

1. Select **Settings**\.  
![\[Application lifecycle settings\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/app-version-lifecycle.png)

1. Select **Enable** for **Lifecycle policy** to enable lifecycle settings\.

1. Select either **Set the application versions limit by total count** or **Set the application versions limit by age**\.

1. If you selected **Set the application versions limit by total count**, enter a value from **1** to **1000** for **Application Versions** to specify the maximum number of application versions to keep before deleting old versions\.

1. If you selected **Set the application versions limit by age**, specify the maximum age, in days from 1 to 180, of application versions to keep\.

1. For **Retention**, specify whether to delete the source bundle from S3 when the application version is deleted\.

1. For **Service role**, specify the role under which the application version is deleted\.

1. Select **Save** to save your application lifecycle settings\.