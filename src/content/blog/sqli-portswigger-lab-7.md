---
author: Nithissh S
pubDatetime: 2024-09-08T15:22:00Z
modDatetime: 2024-09-08T09:12:47.400Z
title: SQL injection attack, listing the database contents on non-Oracle databases
slug: sqli-portswigger-lab-7
featured: false
draft: false
tags:
  - BSCP
  - SQL Injection
description:
  This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables. The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users. To solve the lab, log in as the administrator user. 
---

## Objective 

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.

The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.

To solve the lab, log in as the administrator user. 

## Solution 

Same like the other labs we saw in SQL injection, The product category filter is vulnerable to Possible SQL injection attack

![](../../assets/images/bscp/sqli/sqli31.png)

There are only two columns.. Just like the previous lab 

We were also able to write to both the columns as shown in the image where in the first column we replaced it `NULL` with `abc` and second column `NULL` with `def`

![](../../assets/images/bscp/sqli/sqli33.png)

With the following payload `'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--` we were able the extract the table names from `information.schema` database through the first column and the second column we set it to `NULL` 

![](../../assets/images/bscp/sqli/sqli34.png)

In order to extract the column names from the table `users_mvtqls` we can use the following payload `'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_mvtqls'--` which will actually tells us the column names which is `username_nfnlsh` and `password_vfdfze`

![](../../assets/images/bscp/sqli/sqli35.png)

So, Let's extract the username and password from a particular table using the following payload `'+UNION+SELECT+username_nfnlsh,password_vfdfze+FROM+users_mvtqls--`

As you see in the response, we were able to dump the credentials from the table 

![](../../assets/images/bscp/sqli/sqli36.png)

Logged in as admin and lab is solved 

![](../../assets/images/bscp/sqli/sqli37.png)