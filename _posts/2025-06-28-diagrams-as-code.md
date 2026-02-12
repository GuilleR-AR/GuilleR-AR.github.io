---
layout: post
title: Diagrams as Code
subtitle: Create Diagrams only with your keyboard
gh-repo: GuilleR-AR/diagram-as-code
gh-badge: [star, fork, follow]
tags: [tools, python]
comments: true
mathjax: true
author: Guille R
---
# Weapon of choice

There are multiple tools that can be used to create diagrams using code but the one I went with, that seemed simple enough, it's [Diagrams](https://diagrams.mingrammer.com/).Free, opensource, it is written in Python and it can be installed as a pip package. Even if you don't have too much experience in coding it's not hard to follow.
This doesn't mean it's the best one for you, it certainly has it's quirks, but it seemed the best for my use case.

# Why bother?

This might seem superflous and might be interpetered as overcomplicating things, but I do like to use the diagrams as code whenever possible, here is why:
- It is easily versionable therefore I can keep updating it as needed
- Also since they are in a repository, which is public (if you want to check it out click [here](https://github.com/GuilleR-AR/diagram-as-code/tree/main)), I can reference the images like so:
!["Selfhosted services"](https://raw.githubusercontent.com/GuilleR-AR/diagram-as-code/refs/heads/main/src/apps.png)
- You can even use it to show the progress made between 2 separated versions, for instance:
    - [Old Version](https://raw.githubusercontent.com/GuilleR-AR/diagram-as-code/356473f4cdaecfd0d238dafaa601e7d9e880fc8b/src/network.png):
        !["Old version"](https://raw.githubusercontent.com/GuilleR-AR/diagram-as-code/356473f4cdaecfd0d238dafaa601e7d9e880fc8b/src/network.png)
    - [Current Version](https://raw.githubusercontent.com/GuilleR-AR/diagram-as-code/refs/heads/main/src/network.png):
        !["Current Version"](https://raw.githubusercontent.com/GuilleR-AR/diagram-as-code/refs/heads/main/src/network.png)
- You can even get pretty complex ones like what you see as an example in the Diagrams site
    ![Advanced Example](https://camo.githubusercontent.com/ce6f6ee105140e2e789a4d9b1b727a65f41e2d7a4a0d50b2b8ce417e2fddf784/68747470733a2f2f6469616772616d732e6d696e6772616d6d65722e636f6d2f696d672f616476616e6365645f7765625f736572766963655f776974685f6f6e2d7072656d697365732e706e67)

# Where do I start

Feel free to clone my repo, I included a [Dockerfile](https://github.com/GuilleR-AR/diagram-as-code/blob/main/Dockerfile) and a [docker-compose](https://github.com/GuilleR-AR/diagram-as-code/blob/main/docker-compose.yaml) file to generate the images. You only need to run `docker compose run dac` keep in mind that I reference the file called homelab.py in the CMD of the Dockerfile, if you want to rename it make sure to change that as well.