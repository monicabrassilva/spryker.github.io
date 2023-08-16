---
title: Starting asynchronous commands
description: Learn how to run asynchronous commands
last_updated: May 24, 2022
template: howto-guide-template
---

The Spryker architecture lets you run background asynchronous console commands as scheduled jobs in [Jenkins](/docs/scos/dev/back-end-development/console-commands/console-commands.html#jenkins-setup-commands). Jenkins is available as a Spryker Cloud service. For details about how to use it, see [Cronjobs](/docs/scos/dev/back-end-development/cronjobs/cronjobs.html).

During the deployment, the scheduling of jobs is paused, and the jobs are terminated to roll out a new version. Therefore, long-lasting jobs should be tolerable to interruption and restart.


