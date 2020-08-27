
---
title: "AWS Re:Invent and DevOps"
date: "2012-12-15T13:55:00-04:00"
draft: false
---

2 weeks ago I was in Las Vegas attending [AWS re:Invent](https://reinvent.awsevents.com/). Amazon Web Services is the group responsible for EC2, S3, and other cloud-computing tech and services, they are a part of Amazon.com, the online retailer I'm sure you know. One interesting factoid they touted frequently was that every day, they add the same amount of hardware and infrastructure Amazon.com had in 2003 to their datacenters. This is the first re:Invent, and it had over 5,000 attendees.

The breakout sessions where dense with content and well organized. In particular Netflix's talks on infrastructure and lessons learned were the most interesting. They've developed and <a href="http://netflix.github.com/">open-sourced many tools</a> which I'll have look over in the future. Netflix is the poster-child for success in EC2, and many startups pine to end up working like they do; they're big on the <a href="http://en.wikipedia.org/wiki/DevOps">DevOps</a> style of development and deployment.

Traditionally in growing companies that provide some kind of online service they will have an IT organization that is responsible for the availability and maintenance of existing services; they care about stability and uptime. They may have a Release Engineer that does the deployment part and builds the code that developers write. DevOps (Developer Operations) dispenses with that and instead has the developers do the deployment. For the next few days they'll be responsible for any issues that come up and need to have a rollback plan if services start breaking down; often they'll be on a pager. 

Except for customer data all of their infrastructure is in EC2. They have services running in multiple EC2 regions and availability zones for redundancy. The services are broken up into clusters, which are entities you can define in EC2 to group together running instances (virtual guests). Developers all have the power to create new AMIs and deploy instances into these clusters. Using some of the tools I linked earlier, Netflix engineers are able to shift customer traffic from one instance to another or one cluster to another. This technique allows them to ensure applications are running as expected in production with a small subset of customers before making them widely available.

Another thing that got a lot of people talking was Netflix's <a href="http://arstechnica.com/information-technology/2012/07/netflix-attacks-own-network-with-chaos-monkey-and-now-you-can-too/">Chaos Monkey</a>, which is a service they wrote for EC2 that randomly shuts down running instances. These instances may be serving live customer data! The reasoning is that it ensures the code is resilient and fault tolerant, two attributes that are necessary when you're running services in the Cloud. On the customer end, usually you'll only see a brief increase in latency as the systems figure out where to redirect traffic. Chaos Monkey has been a big success for the company: when instances go down because of hardware issues on Amazon's side, Netflix's service continues uninterrupted reliably.

I probably thought of a dozen cloudy projects while sitting in them and absorbing as much information as I could. Paraphrasing some of the notes I took:

* Use [CloudFormation](https://aws.amazon.com/cloudformation/) to create push-button [Koji](https://fedoraproject.org/wiki/Koji) instances in EC2. [Katello](http://www.katello.org/) already has one, I'm sure other product groups working in the Fedora space would find it useful.
* Similar to the Koji idea, do the same with [AutoQA](https://fedoraproject.org/wiki/AutoQA) for Fedora
* Adding Fedora Koji builders to EC2, and Auto-Scaling them with demand.
* Several ways to improve the RHEL AMIs: better cloud-init integration, adding other AWS tools and libraries to make development (with AWS) easier, KBases on how to make them more durable and fault tolerant in EC2.

I bumped into random folks from Amazon, [OpenStack](http://www.openstack.org/), [CloudStack](https://incubator.apache.org/cloudstack/), and [Nebula](http://opennebula.org/) asking me about future RHEL AMIs and imaging in general. In particular a stock image for OpenStack was on many peoples' minds. (I have heard you and will deliver this!) It was cool to actually be interrogated, and it was gratifying to get more involved in those communities because of past work I've done. I saw Matt Wilson, Max Spevack and other ex-Red Hat too. I posted a G+ pic from the conference.

I also met Matt Miller, the Fedora Cloud Architect. We had dinner together and discussed an array of plans for future imaging work, cloudy projects that would help Fedora, and how to become a better positioned cloud player. Fedora usage is not where it should in this DevOps-centric world, a world that is seriously dominated by Ubuntu. Continuing our current path, I worry Fedora will continue to be passed over by start-ups, and I think we should invest more in making that a more viable distro in the cloud space. After this conference I am thoroughly convinced we're losing mind share on this front.

All in all a great conference, I'd love to attend next year.
