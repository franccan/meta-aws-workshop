---
title: "2 – Build images in a fast and repeatable way"
weight: 10
---
Reproducible builds are a set of software development practices that create a repeatable path from source to binary. The Yocto Project aims to have builds which are entirely reproducible. That is; if you run a build today, then run that same configuration time in the future, the binaries you get out of the build should be identical. 

A simple scenario is that you need to be able to re-run a build at some point in the future and have it succeeded. Yocto also has technology that keeps track of compiled objects. This means when you rebuild, prebuilt artefacts can be used where possible instead of rebuilding from scratch saving time and compute resources. 

In this lab we go through the basics of how AWS CodeBuild, AWS Elastic Container Service (ECR) and AWS Elastic File System (EFS) and you will learn how they can work together with Yocto to produce images in a fast and repeatable way.