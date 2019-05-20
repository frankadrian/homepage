+++
author = "Frank Adrian"
comments = false
cover = ""
date = ""
draft = true
tags = []
title = "Import Yootheme demo content to aws lightsail wordpress instance"

+++
# Easy setup of yootheme worpress on aws lightsail

1. Lauch aws light sail instance
2. connect via ssh
3. `sudo /opt/bitnami/apps/wordpress/bnconfig --disable_banner 1 && `sudo /opt/bitnami/ctlscript.sh restart apache
4. Install YooTheme pro theme: 
5. Active theme
6. Select Customize -> Settings -> Api Key: Enter your api key here, and publish the changes
7. Go to "Homepage Settings" -> Select "A static page" -> "Add New Page" -> name it "home"
8. Go back, select "Builder" -> "Library" and select demo page you want to have 

Repeat step 8 as many times as you require :)