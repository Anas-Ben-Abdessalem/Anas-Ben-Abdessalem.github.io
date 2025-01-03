---
title: " Lab: Reflected XSS into HTML context with nothing encoded"
date: 03-01-2025
categories: [web application  hacking, XSS]
tags: [XSS,web application  hacking, penetration testing, Web App vulnerabilities labs]
description: "This is a simple lab to demonstrate the concept of reflect cross-site Scripting. "
---



## Overview:
This is a simple lab to demonstrate the concept of reflect cross-site Scripting.


## Description:

This lab contains a simple reflected cross-site scripting vulnerability in the search functionality.

To solve the lab, perform a cross-site scripting attack that calls the alert function. 


## Availability of the Lab:
the lab is made by the portswigger academy. you can access it through this link:
https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded


## Methodology:
This lab is simple doesn't need any methodology. It is specific to a single vulnerability. 


## Execution: 

1) The search bar is tested by including the following simple payload in the search field and send it: 

``` <script>alert(1);</script> ```


---> The payload will be reflected giving an alert window.