---
title: " Lab: Stored XSS into HTML context with nothing encoded"
date: 04-01-2025
categories: [web application  hacking, XSS]
tags: [XSS,web application  hacking, penetration testing, Web App vulnerabilities labs]
description: "This is a simple lab to demonstrate the concept of stored cross-site Scripting. "
---



# Overview:
This is a simple lab to demonstrate the concept of stored cross-site Scripting.
Target audience: apprantice


# Description:

This lab contains a stored cross-site scripting vulnerability in the comment functionality.

To solve this lab, submit a comment that calls the alert function when the blog post is viewed. 

Availability of the Lab:
	the lab is made by the portswigger academy. you can access it through this link:
	https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded


# Methodology:
This lab is simple doesn't need any methodology. It is specific to a single vulnerability. 


# Execution: 
1) It is navigated to a post page and tested the comment inputs except the email and the website inputs with the following payload: 

`<script>alert(1);</script>`

- A fake email like (sdsfdfdfr@gmail.com) is included.
- for the website field it is kept empty.

2) The page is refreshed 
result: an alert box is popped-up. 
