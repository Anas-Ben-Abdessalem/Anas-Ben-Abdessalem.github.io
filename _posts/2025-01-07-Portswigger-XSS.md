---
title: " Lab: DOM XSS in jQuery anchor href attribute sink using location.search source"
date: 07-01-2025
categories: [web application  hacking, XSS]
tags: [XSS,web application  hacking, penetration testing, Web App vulnerabilities labs]
description: "This is a simple lab to demonstrate the concept of DOM cross-site Scripting
in jQuery anchor href attribute sink using location.search source"
---




## Overview:
This is a simple lab to demonstrate the concept of DOM cross-site Scripting in jQuery anchor href attribute sink using location.search source.
Target audience: apprentice


## Description:

 This lab contains a DOM-based cross-site scripting vulnerability in the submit feedback page. It uses the jQuery library's $ selector function to find an anchor element, and changes its href attribute using data from location.search.

To solve this lab, make the "back" link alert document.cookie
Availability of the Lab:
	the lab is made by the portswigger academy. you can access it through this link:
	https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-href-attribute


## Methodology:
This lab is simple doesn't need any methodology. It is specific to a single vulnerability. 


## Execution: 

It is navigated to the submit feedback page.
The navigation request is intercepted with burp suite then sent to the repeater:

![image](assets/img/2025-01-07-Portswigger-DOM-XSS/repeater.png)

Going through the document carefully. The following javascript code is descovered:

![image](assets/img/2025-01-07-Portswigger-DOM-XSS/script.png)

The code indicates that the value passed to the returnPath url-paramater 
will be injected to an anchor tag of id "backLink" `<a id="backLink">Back</a>`. This means when including a javascript protocol link like the following:

`javascritpt:alert(document.cookie)`

It will be also injected to it!


**Note:** Note that the document cookie is also injected!


Therefore the following link will be requested:
https://0a04005c033d99bd80d11784001e00e4.web-security-academy.net/feedback?returnPath=javascript:alert(document.cookie)

This sets the backLink to `javascritpt:alert(document.cookie)` which will be executed as a normal js code!
To execute it the back link is then clicked!
In return the following alert is shown with the cookie:
![image](assets/img/2025-01-07-Portswigger-DOM-XSS/cookie.png)