layout: page
title: "How We SRE"
permalink: /how-we-sre
<html><div style="text-align: right">Kerry Knopp<br>
October 9, 2023</div></html>

Below are some elementary principals of how Site Reliability Engeineers (SRE) should try to act.  Not every detail can or should be dictated or described for what we do. These ideas should help guide decisions, so they can be made on the fly, even with top decision makers are out.

## In Brief
* **Repeatability** - Everything is a template.  
* **Ownership** - The cloud infrastructure and SaaS products we own, are ours. Make them easy to maintain and reliable.
* **Responsive** - We want our customers to expect a quick response.  A quick response can be resolving the problem or telling them when to expect a resolution. 
* **Simplicity** - Our toolset is limited on purpose.  But we also want the best tool for the job. We can change tools if it makes sense and there is consensus.
* **Helpful** -  When presented with a problem, we assume it is ours to fix until we can prove otherwise.
* **Secure** - First consider what we're protecting.  Then what users need to get their jobs done.  Move responsibility as far out as necessary.
* **Balance** - Our work is fun and important, but so is our life.  As long as the work is getting done, _when_ it gets done isn't as important.

## In Detail
### Repeatability
When we start using a new resource type in the cloud or a new feature of a tool, our mindset should be making it flexible enough to be reused.  Aspects of reuse are:
* minimize input requirements
* clear but minimal comments
* variables for anything environment or context specific

Examples of things we want to be able to use repeatedly

- terraform or ansible modules
- CI/CD releases (templates and reusable groups)
- kubernetes and configuration yaml

### Ownership
The infrastructure is our responsibility. This means we need to keep it working well, updated and understood.  There are a lot of implications in those 3 things as they apply to cloud resources and SaaS platforms, like the CI/CD and monitoring platforms.

We need to do our best to understand each product we own and maintain at an appropriate level to do so.  There will always be those on our team who know certain things better than others, but there is a minimum level for each resource we need in order to maintain that resource.

When new resources are requested, we need to understand the cost of those resources. The permissions to those resources should be at a level that keeps the cost increases within SRE control - or a manager who accepts that responsibility.  

Examples
- Giving contributor rights at resource group (RG) level allows contributors to create any resources in that RG.
- Blob storage usage can grow over time. Should we set lifecycle policies to delete old stuff?
- Synthetic test on Datadog can get expensive based on frequency of the test


### Responsive
One of the most common complaint that a supporting organization can get is that it takes too long to get a response or a lack of communication.  Users usually ask for things because they need them.  Sometimes they ask for those things 5 minutes after they need them and sometimes they give time to get it done.  Sometimes something is broken.

We want to at least acknowledge a request as soon as we can.  Then keep in communication with the requestor at an appropriate level. If a timeline is provided by us or them and that timeline isn't able to be met, letting them know new expectations is important.

Correcting users - sometimes people don't know, forget or ignore the way we want requests to come in.  We want to correct that behavior, but also provide help at the same time, if possible.  A response to a request that is DM's vs put in the appropriate communications channel might be: "While I start working on that, can you post it to the support channel?"

* In Teams, thumbs up a request if you're going to assume responsibility for it.  If you can't get to it right away or it will take some time to accomplish, let the requestor know; especially if that's not obvious in their request.

### Simplicity
Every tool has it's own language or flow.  Learning new tools takes time out of our days.  Because of this, we want to minimize both the number of tools and the times in which we change them.  This applies both to SRE-specific tools (ansible or terraform) and to the ones we choose for the whole company (Datadog or Snyk).

One way to do this is to ensure we are using each tools features exhaustively.  If there is something we need to do, first look at our existing toolset and see if it can be done effectively with something there.  And as time allows, learn more about each of those tools to see what they are capable of doing.

Finding a balance between the best tool for the job and minimizing the number of tools is also important.  

Example:
* Powershell for Windows and Bash for Linux. We could try and use Powershell for Linux, but it's more limited and would probably still require us using Bash inside the Powershell.  

### Helpful
One problem that led to the DevOps movement is the blame game.  If a developer or other business unit brings a problem or idea to us and it's unclear if it's a problem for us to solve or if "they" need to, we should consider it ours until we're sure it's not and have some pretty clear detail we can give them to point them in the right direction.

SRE is also a good starting point for questions, so we may get some requests that are clearly not ours to solve, but the requestor has no better idea where to start.  In those, steer them to the appropriate place and explain why you're directing them that way.

### Secure
Security is our responsibility.  And the responsibility of every other team too.  Most of the time, secrets are stored in either  Key Vaults or CI/CD pipeline secrets or hidden variables.  As we see users talk about sensitive information, we should help ensure it is protected.

Another way of protecting passwords is to avoid them completely.  In Azure and Entra AD, we have two options and should apply them in this order: Managed Identity and Service Principals. In on premise Active Directory, we have Group Managed Service Accounts (gMSA).  These account types should be used whenever a service account is normally used, but interactive logins are not required.

Examples of sensitive information
* Certificate private keys or PFX files
* API Keys
* passwords

### Balance
We don't require "butts in seats" from 8-5 with a 30 minute lunch, but we do have work to do.  If you're going to be away from your computer at a weird time of day, just let the team know.  Teams status messages are also a great way to do this.

We all have notifications turned on for Teams, which means that our phones will buzz if we're tagged or DM'd while sitting down to dinner. If you're working outside of normal business hours, try to avoid direct messages or tagging specific people unless you have reason to do so.
