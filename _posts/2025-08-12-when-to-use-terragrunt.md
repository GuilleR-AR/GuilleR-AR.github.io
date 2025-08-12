---
layout: post
title: When to use Terragrunt?
subtitle: Still trying to figure it out
tags: [opinion]
comments: true
mathjax: true
author: Guille R
---

# Intro
Some background first, I have been using terraform for almost 6 years, created modules, worked with multiple providers, ran into multiple quirks and even developed some creative workarounds. Even though I knew about terragrunt for almost 3 years it was hard to justify it for me.
I often preferred to use terraform, use plain code with simple scenarios and convert to a module for more complex cases. Rarely saw the case of terragrunt, until...


# Story time...
After a lot of work in a project I was able to import all the instances on prod that were created manually to terraform. Had a module that was creating all the necessary resources and I could create or modify any instance by running a terraform apply. So I had a folder per environment and a single tfvars for all the instances on that environment. Whenever I had to add an instance, I added an extra key to a map of the variable that was beign iterated on the module like so:

### tfvars
```
instances = {
    instance1 {
        key1 = value1
        key2 = value2
    }
    instance2 {
        key1 = value1
        key2 = value2
    }
}
```
### main.tf
```
module "mymodule" {
    for_each = var.instances

name = each.key
key1 = each.value.key1
key2 = each.value.key2

}
```
This was working great so not only we kept adding instances, but also adding to the module more resource per instance, so first we had instances only, then extra disks, then DNS records, then snapshot policies, until... 

# Wild use case appears...
As the tfvars grew bigger and the type of resources also the part of the apply or plan that terraform needs to check what changed started to take longer, since it wasn't that long we carried on, and we kept adding instances and other resources. Until finally we ran in to an issue we couldn't ignore, the cloud provider had a limit of reads per min, and this is a hard limit. So if you made a terraform plan saw that everything looked good and wanted to run a tfapply soon after we would be blocked by the cloud provider for that API read hard limit, and had to wait until the time lapse would allow a re run.
So the path was clear we had to split the instances into different tfstates and tfvars to be allowed to be run separately, but then the question remains "What if i need to update all of them at once?". Everything was pointing to terragrunt, it allowed me to use the DRY (Don't Repeat Yourself) principal and have the backend to be created in base of the folder of the instance, as well as the name and the environment. It took a while and we migrated all of them to terragrunt.
# It was very effective...at first
On the day to day this worked great, we reduced the amount of code, created templates for creating new instances inside a folder with a script and also the time between the command being run and getting the apply reduced, as well as being more legible and predictable. But we ran into some issues when we ran the apply all, the first issue is similar to what we had with the API read limit on the cloud provider, but instead it was with the terraform provider. Since it was downloading the provider version once per instance, so if you did all at once it reached a limit. Luckily there was an easy fix, set a provider cache folder, so if one instance downloaded the provider all the rest shared the same one on that folder. 
That's it right? RIGHT? No, unfortunately I ran into another problem. We started to get DNS issues, at some point the dns server stops resolving some requests, again this is too many requests beign interpreted as some kind of DDoS attack. One alternative I found is to disable the autoapprove on the apply_all command, but it is starting to be more work than it's worth.
# Conclusion
- Am I going back to only using terraform?
    - No, what I may end up doing is to finally get around of implementing pipelines that get triggered per commit on each individual folder and we still keep terragrunt because it saves me a lot of rewriting a lot of repeated code.
- What was the point of all this rant?
    - Basically share what I learned, technically none of the issues I ran into are terragrunt's fault, the feature that made me decide to go with it initially (apply-all command) didn't work out for me .Even though I still don't consider terragrunt to be a bad tool.
- What did I learned from all this?
    1) Sometimes you don't really know a tool until you are deep into the implementation on production.
    2) Even though the feature you wanted didn't worked out as expected learned to appreciate the other ones.   