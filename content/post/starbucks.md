---
title: "Connect to Starbucks Wifi on Arch"
date: 2020-01-10T16:01:44-06:00
draft: False
categories:
  - "tutorial"
tags:
  - "hacks"
comments: true
---
If your browser fails to redirect to the Starbucks login prompt when you join the public Wifi at Starbucks, navigate to: http://www.gstatic.com/generate_204. This is a domain maintained by Google to which Chromium will make a cookieless request and check if the response is redirected. Chromium will then open the redirect target in the assumption that it's a login page, which it is. This was only tested on Chromium. 
