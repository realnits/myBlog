---
author: Nithissh S
pubDatetime: 2024-10-18T15:22:00Z
modDatetime: 2024-10-18T09:12:47.400Z
title: Username enumeration via account lock
slug: auth-portswigger-lab-6
featured: false
draft: false
tags:
  - BSCP
  - Authentication
description:
  This lab is vulnerable to username enumeration. It uses account locking, but this contains a logic flaw. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page. 
---

## Objective 

This lab is vulnerable to username enumeration. It uses account locking, but this contains a logic flaw. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page. 

## Solution 

So I thought we can start with some initial recall by just entering some random username and password like 'xss' as our username and password. As a result, the response says invalid username and password. 

![](../../assets/images/bscp/auth/auth-30.png)

Send this intercepted request to Intruder, and place the placeholder for the username where we need to brute force the username. I took the username wordlist from the lab objective, and didn't proceed with brute forcing the password. Instead, at the end of the password, I just gave the placeholder, and we will be using a different set of credentials called 'cluster bomb attack there'. Repeat the same username for 5 times on the password field as well. 

![](../../assets/images/bscp/auth/auth-31.png)

After starting the brute force attack using Intruder, we found that a new user called `azureuser` with different lengths and other payloads. 

![](../../assets/images/bscp/auth/auth-32.png)

After this, we found the username as `azureuser` and then started a brute-force attack on the password using Intruder (where the resource was 1 concurrent request per second). We found that the password was the `killer` 

![](../../assets/images/bscp/auth/auth-33.png)

The username is `azureuser` and the password is `killer`. After login, the lab is solved. 

![](../../assets/images/bscp/auth/auth-34.png)