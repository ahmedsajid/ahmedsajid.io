---
title: "Deploy Virtual Servers using cURL"
date: 2021-12-04T16:47:59-05:00
tags: ["digitalocean", "Pulumi", "automation", "Terraform"]
layout: post
---

The most popular IaC tool at this point is HashiCorp's [Terraform](terraform.io/). However during my usual internet browsing, I found another Infrastructure-as-Code tool [Pulumi](https://www.pulumi.com/). Its been around for years at this point but I only discovered it very recently.

Pulumi achieves the same thing, Infrastructure-as-Code. However, it uses a different approach. Instead of having to write Terraform HCL files, you can use your favorite programming language such as Python or Go to write code for your infrastructure. This means you no longer have to stitch together different piece of custom written code for different set of tools to manage your platform. You can pick any of the supported Pulumi language and use it to a full end-to-end automation for your platform.

After reading such great things about Pulumi, I wanted to try out Pulumi and really find out the actual benefits of using it.

So I wrote a simple Python Flask application [Droplet Deployer](https://github.com/ahmedsajid/droplet-deployer) which uses Pulumi in the background to make deploying and Droplets on DigitalOcean Cloud as simple as a single `curl` command.

```
curl -H 'Content-Type: application/json' -d '{"name": "<droplet_name>"}' 127.0.0.1:1337/add
```

As you might have realized by now, the applications of Pulumi are endless.

You can use it to write a self-serving portal for your developers that can deploy infrastructure for their use.
Pulumi can be hidden deep within your SaaS providing letting your customers deploy your software on a cloud somewhere with a click of a button. 
Tools can be written using Pulumi embedded within your CI/CD pipelines to manage your code deployments. 
and the list goes on.

For projects at the start out their IaC journey, I would recommend going with Pulumi from the get-go. It takes away the need to learn custom syntax which makes it trivial developers to adopt and get infrastructure deploying within minutes.
