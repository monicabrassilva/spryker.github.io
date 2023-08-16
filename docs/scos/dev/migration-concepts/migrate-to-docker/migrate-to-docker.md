---
title: Migrate to Docker
description: Learn how to convert an existing non-docker based project into a docker based one.
last_updated: Oct 21, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/integrating-the-docker-sdk-into-existing-projects
originalArticleId: 8b072734-58f9-4bcf-8545-676e9f37db7b
redirect_from:
  - /2021080/docs/integrating-the-docker-sdk-into-existing-projects
  - /2021080/docs/en/integrating-the-docker-sdk-into-existing-projects
  - /docs/integrating-the-docker-sdk-into-existing-projects
  - /docs/en/integrating-the-docker-sdk-into-existing-projects
  - /v6/docs/integrating-the-docker-sdk-into-existing-projects
  - /v6/docs/en/integrating-the-docker-sdk-into-existing-projects
  - /v5/docs/integrating-docker-into-existing-projects
  - /v5/docs/en/integrating-docker-into-existing-projects
  - /v4/docs/integrating-docker-into-existing-projects
  - /v4/docs/en/integrating-docker-into-existing-projects
  - /v3/docs/integrating-docker-into-an-existing-project-201907
  - /v3/docs/en/integrating-docker-into-an-existing-project-201907
---

This page describes how you can migrate a non-Docker based project into a Docker based one. If you want to install Spryker from scratch, see [Set up](/docs/scos/dev/set-up-spryker-locally/set-up-spryker-locally.html).

## Install the prerequisites

1. Follow one of the Docker installation prerequisites:
    * [Install Docker prerequisites on MacOS](/docs/scos/dev/set-up-spryker-locally/install-spryker/install-docker-prerequisites/install-docker-prerequisites-on-macos.html)
    * [Install Docker prerequisites on Linux](/docs/scos/dev/set-up-spryker-locally/install-spryker/install-docker-prerequisites/install-docker-prerequisites-on-linux.html)
    * [Install Docker prerequisites on Windows with WSL1](/docs/scos/dev/set-up-spryker-locally/install-spryker/install-docker-prerequisites/install-docker-prerequisites-on-windows-with-wsl1.html).
    * [Installing Docker prerequisites on Windowswith WSL2](/docs/scos/dev/set-up-spryker-locally/install-spryker/install-docker-prerequisites/install-docker-prerequisites-on-windows-with-wsl2.html).

2. Install the [Spryker Core](/docs/pbc/all/miscellaneous/{{site.version}}/install-and-upgrade/install-features/install-the-spryker-core-feature.html) feature.

## Set up .dockerignore

Create a new `.dockerignore` file to match the project file structure:

```yaml
.git
.idea
node_modules
/vendor
/data
!/data/import
.git*
.unison*
/.nvmrc
/.scrutinizer.yml
/.travis.yml
/newrelic.ini

/docker
!/docker/deployment/
```

To learn more about the structure of the file, see [.dockerignore file](https://docs.docker.com/engine/reference/builder/#dockerignore-file).

## Set up configuration

In `config/Shared`, adjust or create a configuration file. The name of the file should correspond to your environment. See [config_default-docker.php](https://github.com/spryker-shop/b2c-demo-shop/blob/master/config/Shared/config_default-docker.dev.php) as an example.

## Set up a deploy file

Set up a [deploy file](/docs/scos/dev/the-docker-sdk/{{site.version}}/deploy-file/deploy-file-reference-1.0.html) per your infrastructure requirements using the examples in the table:

| DEVELOPMENT MODE | DEMO MODE |
| --- | --- |
| [B2C Demo Shop deploy file](https://github.com/spryker-shop/b2c-demo-shop/blob/master/deploy.dev.yml) | [B2C Demo Shop deploy file](https://github.com/spryker-shop/b2c-demo-shop/blob/master/deploy.yml) |
| [B2B Demo Shop deploy file](https://github.com/spryker-shop/b2b-demo-shop/blob/master/deploy.dev.yml) | [B2B Demo Shop deploy file](https://github.com/spryker-shop/b2b-demo-shop/blob/master/deploy.yml) |

## Set up the installation script

In `config/Shared`, prepare the installation recipe that defines the way Spryker should be installed.

Use the following recipe examples:

* [B2B Demo Shop installation recipe](https://github.com/spryker-shop/b2b-demo-shop/blob/master/deploy.yml)
* [B2C Demo Shop installation recipe](https://github.com/spryker-shop/b2c-demo-shop/blob/master/deploy.yml)

## Install the Docker SDK

1. Clone the Docker SDK:

```bash
git clone https://github.com/spryker/docker-sdk.git ./docker
```

2. Initialize docker setup:

```bash
docker/sdk bootstrap
```

{% info_block infoBox "Bootstrap" %}

Once you finish the setup, you don't need to run `bootstrap` to start the instance. You only need to run it after updating the Docker SDK or changing the deploy file.

{% endinfo_block %}

3. Build and run the application:

```bash
docker/sdk up
```

{% info_block warningBox %}

Make sure that, in the `hosts` file, all the domains from `deploy.yml` are defined as `127.0.0.1`.

{% endinfo_block %}


## Endpoints

To verify that the migration is successful, make sure you can access the endpoints configured in the deploy file. To learn about the deploy file, see [Deploy file reference - 1.0](/docs/scos/dev/the-docker-sdk/{{site.version}}/deploy-file/deploy-file-reference-1.0.html).

{% info_block infoBox "RabbitMQ UI credentials" %}

To access RabbitMQ UI, use `spryker` as a username and `secret` as a password. You can adjust the credentials in `deploy.yml`.

{% endinfo_block %}

## Get the list of useful commands

To get the full and up-to-date list of commands, run `docker/sdk help`.

## Next steps

* [Troubleshooting](/docs/scos/dev/set-up-spryker-locally/troubleshooting-installation/troubleshooting-installation.html)
* [Debugging Setup in Docker](/docs/scos/dev/the-docker-sdk/{{site.version}}/configuring-debugging-in-docker.html)
* [Deploy File Reference - 1.0](/docs/scos/dev/the-docker-sdk/{{site.version}}/deploy-file/deploy-file-reference-1.0.html)
* [Services](/docs/scos/dev/the-docker-sdk/{{site.version}}/configure-services.html)
* [Self-signed SSL Certificate Setup](/docs/scos/dev/set-up-spryker-locally/configure-after-installing/set-up-a-self-signed-ssl-certificate.html)
* [Adjust Jenkins for a Docker environment](/docs/scos/dev/migration-concepts/migrate-to-docker/adjust-jenkins-for-a-docker-environment.html)
