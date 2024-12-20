---
author: Nithissh S
pubDatetime: 2024-10-28T15:22:00Z
modDatetime: 2024-10-28T09:12:47.400Z
title: Remote code execution via web shell upload
slug: fu-portswigger-lab-1
featured: false
draft: false
tags:
  - BSCP
  - File Upload Vulnerabilities
description:
  This lab contains a vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem. To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner. You can log in to your own account using the following credentials `wiener:peter`
---

## Objective 

This lab contains a vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem.

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter` 

## Solution

Once after signing with the credentials provided in the lab objective, we can able to login as a `wiener`. Going through the profile, we found that there is a certain functionality where we can able to upload an avatar. 

![](../../assets/images/bscp/fileupload/fu-1.png)

We were able to find that you can upload the file at any time. For example, I did with the text file. It worked out, and so I created the following PHP exploit where it gets the content from `/home/carlos/secret` which is our endgoal 

```php
<?php echo file_get_contents('/home/carlos/secret'); ?>
```

Now let's open the avatar in new tab and which will be available in the following path `/files/avatars/exploit.php` and executed the following php code and shown the contents of `/home/carlos/secret` and this is content: `CkFkrsSWe8c2A9HGZLFjfjLDOnDHlZP6`

![](../../assets/images/bscp/fileupload/fu-2.png)

Submitting the code as a solution will solve the lab. 

![](../../assets/images/bscp/fileupload/fu-3.png)