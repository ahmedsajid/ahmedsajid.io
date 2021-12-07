---
layout: post
date: 2021-09-20T09:00:00-05:00
title: Simple cron monitoring using healthchecks.io
tags: ["healthchecks.io", "monitoring", "cron", "automation", "ansible"]
---

While working on home server automation, I came across the awesome Open Source project [healthchecks](https://github.com/healthchecks/healthchecks).

I had been looking for a simple way to monitoring my [Ansible home automation setup](https://github.com/ahmedsajid/home-setup) that is triggered via cron and send me alerts if my home automation takes longer than a set interval or just fails.

[healthchecks.io](https://healthchecks.io), the service for healthchecks project, is an extremely simple dashboard for setting up monitoring. It also has integration with alerting systems as well as commonly used communication tools such as Teams, Slack, Signal and numerous others.

From project's [website](https://healthchecks.io/docs/):

> Healthchecks.io works as a dead man's switch for processes that need to run continuously or on a regular, known schedule.

That means if the results are received within given amount of time at regular intervals, the check is considered healthy, if not the check has failed. 

Results can be submitted using `curl` command embedded within your script.

```shell
# Add at the end of your script
# check-uuid - custom uuid generated for your check
curl https://hc-ping.com/check-uuid
```

It also supports signals such as `start` to indicate start of script or a job and `fail` to indicate failure.

```shell
# Beginning of your script
curl https://hc-ping.com/check-uuid/start

##################
# YOUR TASKS HERE
##################

# Towards the end of the script

if [ $? -eq 0 ]
then 
    # Post success
    curl https://hc-ping.com/check-uuid
else 
    # Post failure
    curl https://hc-ping.com/check-uuid/fail
fi
```

A full range of supported API calls can be found [here](https://healthchecks.io/docs/http_api/).

healthchecks.io also supports [submitting logs](https://healthchecks.io/docs/attaching_logs/) which can then be part of the alert message.

healthchecks.io is trivial to setup and easy to management. Initial setup is extremely simple, it has great range of features and documentation is well written. Here's a [link](https://github.com/ahmedsajid/home-setup/blob/3bff751ac52af4ef7842fa8b9cf065d9e7260f36/ansible/callback_plugins/healthchecks.py) to Ansible callback plugin that I'm using to integrate with healthchecks.io. 
