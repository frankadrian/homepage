+++
author = "Frank Adrian"
comments = true
cover = "/uploads/Easy setup of yootheme worpress on aws lightsail.png"
date = 2019-05-20T16:36:00Z
tags = ["wordpress", "yootheme"]
title = "Easy setup of yootheme wordpress on aws lightsail"

+++

1. Lauch aws light sail instance
2. connect via ssh
3. `sudo /opt/bitnami/apps/wordpress/bnconfig --disable_banner 1 && sudo /opt/bitnami/ctlscript.sh restart apache`
4. to enable https: `sudo /opt/bitnami/bncert-tool` and follow the prompts

### Install "YooTheme pro" theme

1. Download the Wordpress theme from [https://yootheme.com/pro](https://yootheme.com/pro "https://yootheme.com/pro")
2. Install and active the theme
3. To add your API Key select "Customize" -> "Settings" -> "Api Key": Enter your api key here, and publish the changes

### Add static pages with yootheme demo content

1. Go to "Homepage Settings" -> Select "A static page" -> "Add New Page" -> name it "home" or what ever you like
2. Go back, select "Builder" -> "Library" and select demo page you want to have, publish the changes and you can start customising the pages

Repeat step 8 as many times as you require :)