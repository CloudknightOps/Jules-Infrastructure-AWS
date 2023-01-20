# Jules-Infrastructure-AWS-WebApplication

This CloudFormation template deploys a load balancer and its dependencies needed to host the Udagram web application. The template includes security groups, an autoscaling group with its required launch configuration, target groups, and an IAM role for the compute instances.

## Parameters

- **EnvironmentName**: A name that will be prefixed to resource names to enable easy identification. This is a string parameter.

## Resources

The template creates the following resources:

- **UdacityS3ReadOnlyEC2**: An IAM role that allows read-only access to Amazon S3 and full access to Amazon SSM.
- **ProfileWithRolesForApp**: An IAM instance profile that references the UdacityS3ReadOnlyEC2 role.
- **LBSecGroup**: A security group for the load balancer that allows incoming HTTP traffic.
- **WebServerSecGroup**: A security group for the web servers that allows incoming HTTP traffic and allows all outgoing traffic.
- **WebAppLaunchConfig**: A launch configuration for the web servers that includes user data to install Apache and display a "It Works!" message.
- **WebAppGroup**: An autoscaling group that uses the WebApp
LaunchConfig and is associated with the target group.
- **WebAppLB**: A load balancer that forwards incoming HTTP traffic to the web servers.
- **WebAppTargetGroup**: A target group that the load balancer forwards traffic to.

## Usage

To use the template, you will need to have the AWS CLI installed and configured with appropriate credentials.

1. Download the template from the repository.
2. Use the AWS CLI to create a new stack, specifying the template file and any desired parameter values:
3. Monitor the stack creation progress and events using the AWS CLI or the CloudFormation console.

## Note
Please make sure to check and update the parameter values before running the scripts as per your requirement. Also, please update the ami-id as per the region you are running it. Also, You should check the `SecurityGroupIngress` and `SecurityGroupEgress` rules, as the current settings allow all incoming and outgoing traffic on port 80 which may not be appropriate.

## Contribution
Feel free to contribute to this repository by creating a pull request with any updates or changes you would like to make.
