---
author: Nithissh S
pubDatetime: 2024-12-02T15:22:00Z
modDatetime: 2024-12-02T09:12:47.400Z
title: Limit overrun race conditions
slug: race-portswigger-lab-1
featured: false
draft: false
tags:
  - BSCP
  - Race Condition
description:
  This lab's purchasing flow contains a race condition that enables you to purchase items for an unintended price. To solve the lab, successfully purchase a Lightweight L33t Leather Jacket.You can log in to your account with the following credentials `wiener:peter`. 
---

## Objective 

This lab's purchasing flow contains a race condition that enables you to purchase items for an unintended price.

To solve the lab, successfully purchase a Lightweight L33t Leather Jacket.

You can log in to your account with the following credentials: `wiener:peter`. 

## Solution 

Once after spinning the lab, we will see a promo code in our home page 

![](../../assets/images/bscp/race/race-1.png)

Now, we will take the leather jacket.. add it to cart and apply the coupon.. and now we can intercept the request and this is how it looks like 

![](../../assets/images/bscp/race/race-2.png)

Now we can send the same tab for `27` times in repeater and add it to a particular tab group actually 

![](../../assets/images/bscp/race/race-3.png)

After that, now send the request.. in an group in parallel actually meaning at the same time and exact moment.. request is sent in parallel.. once after the request passes through, where it will say `Coupon is applied` for all the `27` tabs actually and now seeing in the UI part, we can see product price is reduced significantly 

![](../../assets/images/bscp/race/race-4.png)

Now place the order where in earlier the price was `1337$` which is reduced to `30$` due to fact that we have actually `20% off` promo code.. for 27 times, which will actually solve the lab 

![](../../assets/images/bscp/race/race-5.png)