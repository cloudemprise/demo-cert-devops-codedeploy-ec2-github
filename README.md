# demo-cert-devops-codedeploy-sample-github

> The repository contains artifacts and reference material related to an AWS CodeDepoly deployment project and its auxiliary components. These components relate to a dual GitHub & AWS CodeCommit repository that is used to perform an AWS CodeDeploy infrastructure sampling.

---

#### Overview

This repository contains artifacts and reference material related to an AWS CodeDeploy demonstration that deploys a sample application revision from a GitHub repository to a single Amazon EC2 instance running Amazon Linux 2. It elaborates on the following tutorial: [Use CodeDeploy to deploy an application from GitHub](https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorials-github.html)

#### Integrating CodeDeploy with GitHub

CodeDeploy supports GitHub. AWS CodeDeploy can deploy application revisions stored in GitHub repositories for type EC2/On-Premises deployments only. The authorization process involves interacting with the AWS Console to give each application permission using OAuth.


#### AWS CodeDeploy Agent

For type EC2/On-Premises deployments, the AWS CodeDeploy service requires that an agent be installed on the target instance. The CodeDeploy agent communicates outbound using HTTPS over port 443 and is not required for deployments that use the Amazon ECS or AWS Lambda compute platform. Log file can be found here: /var/log/aws/codedeploy-agent.

For the simplicity of convenience, this demonstration manually installs the agent via the Userdata Script facility of the Launch Template CloudFormation nested stack.

This agent could very well be be installed using AWS Systems Manager and is in fact the recommended method for installing and updating the CodeDeploy agent. There is a very handy AWS Systems Manager service integration that can set up installation and scheduled updates via the AWS Console when you manually create a Deployment Group. Don't forget to include the Managed Policy: AmazonSSMManagedInstanceCore within your service role.

#### Infrastructure As Code

A stand-alone solution records the complete infrastructure definition and takes the form of nested AWS CloudFormation templates. These are provisioned via a bash script that orchestrate the creation of all the Cloud resource components required in this demonstration and comprise the following:


```bash

automation/
├── cfn-templates
│   ├── demo-cert-devops-codedeploy-sample-github-cfn-dev-deploy.yaml.(DEPLOYMENT)
│   ├── demo-cert-devops-codedeploy-sample-github-cfn-ec2-lt.yaml.....(LAUNCH TEMPLATE)
│   ├── demo-cert-devops-codedeploy-sample-github-cfn-ec2-pub.yaml....(EC2 INSTANCE)
│   ├── demo-cert-devops-codedeploy-sample-github-cfn-iam.yaml........(IAM ROLES)
│   ├── demo-cert-devops-codedeploy-sample-github-cfn-vpc-sg.yaml.....(SECURITY GROUP)
│   ├── demo-cert-devops-codedeploy-sample-github-cfn-vpc.yaml........(VPC)
│   └── demo-cert-devops-codedeploy-sample-github-cfn.yaml............(TOP LEVEL)
└── provision-infrastructure-cfn-templates.sh.........................(BASH SCRIPT)

```

--- 

#### Reference:


- AWS CodeDeploy - [GitHub integration with CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/integrations-partners-github.html).

- AWS CodeDeploy - [Connect a CodeDeploy application to a GitHub repository](https://docs.aws.amazon.com/codedeploy/latest/userguide/deployments-create-cli-github.html)

- GitHub - [Authorizing OAuth Apps](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/authorizing-oauth-apps)

- AWS CodeDeploy - [Install the CodeDeploy agent using AWS Systems Manager](https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-ssm.html)



#### Relevant APIs:

> ##### _AWS CodeDeploy_

> [create-application](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/deploy/create-application.html)

> [create-deployment-group](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/deploy/create-deployment-group.html)

> [create-deployment](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/deploy/create-deployment.html)

> [create-deployment-config](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/deploy/create-deployment-config.html)

> [get-deployment-instance](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/deploy/get-deployment-instance.html)

> [get-deployment-config](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/deploy/get-deployment-config.html)

--- 

> [push](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/deploy/push.html)
