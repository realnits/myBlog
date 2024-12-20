---
author: Nithissh S
pubDatetime: 2024-10-28T15:22:00Z
modDatetime: 2024-10-28T09:12:47.400Z
title: Web shell upload via path traversal
slug: fu-portswigger-lab-2
featured: false
draft: false
tags:
  - BSCP
  - File Upload Vulnerabilities
description:
  This lab contains a vulnerable image upload function. The server is configured to prevent execution of user-supplied files, but this restriction can be bypassed by exploiting a secondary vulnerability. To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner. You can log in to your own account using the following credentials `wiener:peter` 
---

## Objective 

This lab contains a vulnerable image upload function. The server is configured to prevent execution of user-supplied files, but this restriction can be bypassed by exploiting a secondary vulnerability.

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter` 

## Solution 

So just like the last lab, we have the same functionality to upload an avatar. Once after uploading, viewing the avatar image in new tab (usually in the last lab) shows the payload execution, but in this lab, it shows a blank page app. 

![](../../assets/images/bscp/fileupload/fu-4.png)

Intercept the request when you upload the avatar and change the filename from `exploit.php` to `..%2fexploit.php` And now once we change it and send the request, it will upload the files inside `/files` directory rather than `/files/avatars`

![](../../assets/images/bscp/fileupload/fu-5.png)

Now open the uploaded file which is inside the `/files` directory through the browser where it will show the contents of `/home/carlos/secret` due to fact that our php code got successfully executed 

![](../../assets/images/bscp/fileupload/fu-6.png)

Just copy the code and submit it as solution, and that will solve the lab. 

![](../../assets/images/bscp/fileupload/fu-7.png)