---
title: " Lab: DOM XSS in innerHTML sink using source location.search"
date: 06-01-2025
categories: [web application  hacking, XSS]
tags: [XSS,web application  hacking, penetration testing, Web App vulnerabilities labs]
description: "This is a simple lab to demonstrate the concept of DOM cross-site Scripting
in innerHTML sink using source location.search."
---




## Overview:
This is a simple lab to demonstrate the concept of DOM cross-site Scripting in innerHTML sink using source location.search.
Target audience: apprentice


## Description:

This lab contains a DOM-based cross-site scripting vulnerability in the search query tracking functionality. It uses the JavaScript document.write function, which writes data out to the page. The document.write function is called with data from location.search, which you can control using the website URL.

To solve this lab, perform a cross-site scripting attack that calls the alert function. 
Availability of the Lab:
	the lab is made by the portswigger academy. you can access it through this link:
	https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink


## Methodology:
This lab is simple doesn't need any methodology. It is specific to a single vulnerability. 


## Execution: 
First the search box is tested with the simple payload `<script>alert(1)</script>` and is intercepted with burp suite proxy.
Then the intercepted request is sent to the Repeater.


![Image](../assets/img/2025-01-06-Portswigger-DOM-XSS/repeater.png)


The payload didn't return the desired response but while examining the response the following javascript code is discovered:


![image](../assets/img/2025-01-06-Portswigger-DOM-XSS/script.png)


This script exposes a potential information that the innerHTML property of the div tag of id = "searchMessage" is assigned the location.search property of the window object which means that testing directly from the web page is much better because it will also include testing the window object!


The search element is directly tested from the web page with the mentioned payload. 
As a result the alert box pop-up!
