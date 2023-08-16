---
title: Environment provisioning
description: This document explains core concepts that are important to understand before filing an environment provisioning request.
last_updated: Mar 14, 2023
template: concept-topic-template

---

Before proceeding with the provisioning of your Spryker PaaS environment, we would like to clarify the information we require from you. To initiate the environment provisioning process, you need to create a case using your support portal access. If you have questions, visit the [Spryker Support Portal](https://support.spryker.com). If you don't have access to the support portal yet, request it through the [request form](https://www.surveymonkey.com/r/XYK5R26) on SurveyMonkey. 
Once you are logged in to the Spryker Support Portal, you can submit the [environment provisioning request](https://support.spryker.com/s/hosting-change-requests/change-request-new-environment).

{% info_block warningBox %}

This process can only be initiated through a customer account. To request an environment, partners should work with their respective customers.

{% endinfo_block %}

The following sections outline the information you need to provide to initiate provisioning of your environment. 

{% info_block warningBox "Mandatory information" %}

Please note that all sections without the word "Optional" in their title are mandatory for the provisioning request to be processed.

{% endinfo_block %}

## Environment

This section explains how different attributes of your environment are used.

### Optional: Environment name

The environment name is derived from the combination of the project name and environment type. The environment name is referenced in AWS services endpoints:
* Redis
* DB
* Elasticsearch
* Deploy files
* S3 buckets

### Project name

The *project name* is the name of the customer or the customer's preferred name for their project. The project name can't be modified once the environment is provisioned. It shouldn't contain special characters or spaces.

**Recommended:** myshop

**Not recommended:** myshöp, my shop, my-shop, my$shop

### Environment type

The *[environment type](/docs/cloud/dev/spryker-cloud-commerce-os/environments-overview.html)* corresponds to the popular naming convention for environment tiers in software development. You can refer to your contract for information on what environments you are entitled to and choose the respective one—for example:

Lower environments: STAGE, DEV

Production: PROD-LIKE, PROD

**Example:**

If `myshop` is the customer, then `myshop-PROD` is an environment name, where `myshop` is the project name, and `PROD` is the environment type.

### AWS region

The *AWS region* indicates where customers want their infrastructure resources to be available. For more information about available options for the AWS region, refer to the AWS [official documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html). For information about the AWS region you are entitled to use, check your contract. 

The following AWS regions are supported:
- Asia Pacific (Tokyo)
- Asia Pacific (Seoul)
- Asia Pacific (Mumbai)
- Asia Pacific (Singapore)
- Asia Pacific (Sydney)
- Canada (Central)
- Europe (Frankfurt am Main)
- Europe (Stockholm)
- Europe (Milan)
- Europe (Ireland)
- Europe (London)
- Europe (Paris)
- South America (São Paulo)
- US East (Ohio)
- US East (N. Virginia)
- US West (N. California)
- US West (Oregon)


## Code base and boiler plates

This section explains the aspects of the code base and boilerplate you use and its impact on the provisioning task.

### Code base

Which code base is being used? As Spryker offers different business models based on customer requirements, application services related to infra setup vary based on the model. It is important to know which model is being used for the respective environment during provisioning. 

{% info_block infoBox "Note" %}

Similar to project names, you can't switch between these models after the environment is created. Switching means a complete de-provisioning of your environment. You can't carry over any data—for example, B2B, B2C, B2B Marketplace, or B2C Marketplace.

{% endinfo_block %}

### Repository

The repository is the place where the customer's Spryker application code resides. Spryker supports only GitHub, GitLab, and Bitbucket code hosting services. If the customer code base isn't ready, the Spryker team provisions the environment with the previously chosen Demo Dhop model from the most recent release using GitHub.

GitHub: If the customer uses GitHub, provide a link to the GitHub repository, including a branch and a valid GitHub token. This allows code pipelines to access the repository. Ensure that you securely share the GitHub token according to [Spryker recommendations](/docs/scos/user/intro-to-spryker/support/how-to-share-secrets-with-the-spryker-support-team.html).

GitLab and Bitbucket: Connecting GitLab and Bitbucket repositories directly to pipelines isn't supported. Therefore, we have to enable the codecommit feature during provisioning. Connections with pipelines can be established only after the environment is provisioned. If possible, grant GitLab or Bitbucket access to the Spryker engineer working on this request. If not, we'll use your deploy file along with the Spryker Demo Shop during provisioning. For detailed information about the connection process, see [Connect a GitLab code repository](/docs/cloud/dev/spryker-cloud-commerce-os/connecting-a-code-repository.html#connect-a-gitlab-code-repository) section in "Connecting a code repository".

{% info_block infoBox "Note" %}

We can share the required credentials mentioned in the preceding documentation only after environment provisioning is complete.

{% endinfo_block %}

### Deploy file

The *Deploy file* is a YAML file used by the Docker SDK to build infrastructure for applications. If the customer provides their own repository, a deploy file must be provided. For Demo Shop deployments, Spryker Cloud Ops prepares the file on their own. A repository usually has multiple deploy files that are relevant for different purposes and environments. Demo Shops have a `deploy.dev.yml` file that is mostly meant for local development purposes. The naming of these files is important. The naming convention is `deploy.{PROJECT_NAME}-{ENVIRONEMENT_NAME}.yml`—for example, `deploy.myshop-production.yml`. For reference, see [Deploy file](/docs/scos/dev/the-docker-sdk/{{site.version}}/deploy-file/deploy-file.html). The most relevant deploy file that you can use as a reference is [deploy.aws-env-template.yml](https://github.com/spryker-shop/b2b-demo-shop/blob/master/deploy.aws-env-template.yml). Each Demo Shop repository has its respective deploy file template. Adjust this according to your requirements and preferences following the preceding documentation and share it with Spryker.

## Domains

This section explains how you can choose a domain name for your project. The domain name determines the URL under which your shop will be available.

### Domain name

A domain name must be set for the environment. If not provided, it is a default non-public Spryker domain—for example, `myshop-production.cloud.spryker.toys`. Domain names can be changed later. However, if you already know a domain for the application, you can specify this domain in your `deploy.yml` files. During the provisioning process, we provide you with CNAMES and validation records that you can set in your DNS management. The validation records let us provide an SSL certificate for you, and the CNAME records point your domain to the public DNS name of the load balancers responsible for your environment, effectively directing visitors to that domain to your Spryker application.
Please note Spryker is only issuing SSL certificates for endpoints that are managed by the Spryker Cloud Commerce.

## User access

Customer or partner users must have access to the following entities:
* AWS Console access: You can use it to access environment CloudWatch logs, deployment pipelines, parameter store, S3 buckets. Provide the email addresses of users who need access to AWS Console.
* VPN: You can use it to access services such as databases, Jenkins, and RabbitMQ. Usually, developers or DevOps personnel need it. Provide the email addresses of users that need VPN access.
* SSH: You can use it to access the Bastion Host, and from there, reach other services via [port forwarding](/docs/cloud/dev/spryker-cloud-commerce-os/access/connecting-to-services-via-ssh.html). Usually, developers or DevOps personnel need it in special cases. Provide an SSH public key and email addresses of users who need access to SSH. Keep in mind that VPN access is required to use SSH.
* SFTP: This access is required for the SFTP Bastion Host. Provide an SSH public key and email addresses of users who need access to SFTP. Keep in mind that VPN access is required to use SFTP. Please note that SFTP is not provisioned by default.

## Optional: Additional attributes

This section explains what additional attributes you can specify at the beginning of your provisioning, as well as accesses you can request.

### Optional: SFTP
Spryker implemented SFTP on top of EFS. You can use SFTP for any third-party integrations or for explicit data imports via Jenkins jobs if required on the project level. Note that SFTP is only available on Bastion and Jenkins. This feature is disabled by default. You can also request it later via the support ticket, but it is preferred to validate this option during provisioning.

### Optional: Site to Site VPN
A Site-to-Site VPN (Virtual Private Network) is a type of network connection that enables secure communication between two or more geographically separated networks. This type of VPN allows two or more sites to establish a secure and encrypted connection over the internet or other public networks, creating a virtual private network between the two sites. 
The following configuration parameters are required to set up the Site-to-Site VPN tunnel:
- Customer gateway IP address
- IP ranges on the customer side that would need access to Spryker VPC
The following configuration parameters are optional:
- Device name on customer gateway
- Custom BGP(Border Gateway Protocol) ASN
- Dynamic BGP routes
- Other Parameters of tunnels

{% info_block infoBox "IPsec" %}

If you need IPsec, provide your internal subnet CIDR, so our Spryker VPC doesn’t overlap with it. It is crucial to evaluate this option during provisioning, as Spryker can’t change it later once the environment is provisioned. If overlapping is identified, the environment will need to be recreated.

{% endinfo_block %}

### Optional: Default network settings
Each Spryker Cloud Commerce environment uses a dedicated Virtual Private Cloud (VPC).
The default CIDRs are the following:
- For the first non-production environment: 10.105.0.0/16.
- For the first production environment: 10.106.0.0/16.
- Any next environment, regardless if it is a production or non-production one, will be in the range 10.107.0.0/16 - 10.200.0.0/16
The default CIDR can be changed based on your request. Please make sure you let Spryker know about it while requesting an environment.

### Optional: Clone environment
In case you would like to clone an existing environment and use the predefined setup there (e.g. access rights, DB), please mention it in your request.
