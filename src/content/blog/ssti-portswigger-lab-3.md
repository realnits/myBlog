---
author: Nithissh S
pubDatetime: 2024-12-03T15:22:00Z
modDatetime: 2024-12-03T09:12:47.400Z
title: Server-side template injection using documentation
slug: ssti-portswigger-lab-3
featured: false
draft: false
tags:
  - BSCP
  - SSTI
description:
  This lab is vulnerable to server-side template injection. To solve the lab, identify the template engine and use the documentation to work out how to execute arbitrary code, then delete the morale.txt file from Carlos's home directory. You can log in to your own account using the following credentials `content-manager:C0nt3ntM4n4g3r`
---

## Objective 

This lab is vulnerable to server-side template injection. To solve the lab, identify the template engine and use the documentation to work out how to execute arbitrary code, then delete the morale.txt file from Carlos's home directory.

You can log in to your own account using the following credentials: `content-manager:C0nt3ntM4n4g3r`

## Solution 

Once after login as `content-manager` we can edit the displayed products and from that we have a functionality called `Edit template` where can edit the product descriptions and alot more to play around 

I entered something `${nithissh}` there isn't a predefined value in it and which will eventually gets crashed and show an error response as `Freemarker` template which is part of Java 

![](../../assets/images/bscp/ssti/ssti-10.png)

Now, with the following payload `${"freemarker.template.utility.Execute"?new()("id")}` we can see that `id` command got successfully executed in here 

![](../../assets/images/bscp/ssti/ssti-11.png)

In order to solve the lab, we can pass the following payload `${"freemarker.template.utility.Execute"?new()("rm /home/carlos/morale.txt")}` which will delete the file mentioned in the lab objective and that solves the lab 

![](../../assets/images/bscp/ssti/ssti-12.png)