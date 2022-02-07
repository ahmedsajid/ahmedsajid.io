---
title: "Jenkins EC2 plugin worker AMI selection based on Resource Tags"
date: 2022-02-06T22:00:00-05:00
tags: ["Jenkins", "Build", "EC2", "AMI", "AWS"]
layout: post
---

TL;DR, Jenkins EC2 plugin has the option for worker AMIs to be selected based on Tags and NOT just a hardcoded AMI ID. This comes in handy when you have an automated build pushing out AMIs with the same tags on regular basis, eliminating the need for manually updating hardcoded AMI to latest version in Jenkins EC2 cloud configuration.

Long version......

Most companies managing their own Jenkins CI Build system on AWS Cloud must be familiar with the [ec2-plugin](https://plugins.jenkins.io/ec2/).

During my recently experience with a Jenkins setup, I found that AMI IDs were hardcoded pointing to images that were built 2 years ago. This stood out to me as a security issue, something to be dealt with right away.

I went on a journey to figure out how to automate the process of changing the AMI on regular basis with ID of latest AMI available. Since the AMI build job already existed, all I had to do was to introduce a post-build step to update Jenkins Cloud configuration with a newly built AMI. 

Simple, right? Yeah it seemed the same to me, when I came across this [PR](https://github.com/jenkinsci/ec2-plugin/pull/154). Some of the folks came up with a great solution which works, but has a downside. You will have to 'Approve' this script within Jenkins as it considers it dangerous and might pose a security problem.

Approving something that can have negative consequences, just didn't sound like a great solution. I wasn't ready to compromise on security to have a piece of automation to solve this issue.

After a few days of researching, I came across this [JIRA](https://issues.jenkins.io/browse/JENKINS-63917). This particular individual was having same issue when another user pointed to a feature that might help.

For those have worked with such a setup before probably know a simpler solution, which as you can see, I didn't find until much later in the game.

I feel that this is one of the GREAT features of this plugin and I was unable to find any documentation around it. I could have simply provided a list of tags to filter AMIs by and based on these tags, the plugin looks up the AMI to be the Jenkins Worker node on EC2. If there are more than 1 AMIs matching the filter, it will choose the one with latest creation date.

<p align="center">
  <img src="/img/JenkinsEC2TagsFiltering.jpg" alt="Jenkins EC2 Plugin AMI Filtering based on Resource Tags">
</p>

In this example you can see that I have specified multiple tags such as `name`, `builder` and `os` and their values as the AMI Filters.

You could say that I wasn't just looking hard enough. You would be correct! I wasn't looking hard enough in the right place.

I hope this helps someone else going through the same struggles of figuring out this problem.

For more info see the actual [PR](https://github.com/jenkinsci/ec2-plugin/pull/533) which implemented this great feature.