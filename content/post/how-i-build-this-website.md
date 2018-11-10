+++
author = "Frank Adrian"
comments = false
cover = ""
date = "2018-11-10T13:13:38+00:00"
draft = true
tags = ["web development", "aws", "hugo"]
title = "How I build this website"

+++
This post outlines how I initially built this website, using a couple of services and open source projects, all in the cloud and completely for "free" (exluding the domain name (you could use github pages for free) and provided you stay in the [free tier](https://aws.amazon.com/free/?awsf.Free%20Tier%20Types=categories%23alwaysfree)).

<!--more-->

Tools I use:

* [hugo](https://gohugo.io/) using the [nuo theme](https://github.com/laozhu/hugo-nuo)
* github
* [forestry](https://forestry.io/)
* AWS

## An overview of the services

### Hugo

is a static website generator, I had heard about this project a couple of years ago and came across it again recently and was really happy with the way it has developed. So I decided to test this and see how easy it is to set up a page.

This service makes it, as they state, fun again to develop a website. One big advantage is that it is SEO optimised by default compared to SPA frameworks like Angular.

Till now I can only agree with their statement as it was very easy (as a Web-developer) to set up this website.

### Github

is used only to store the source code. You can choose any of your favourite VCS provider.

### Forestry

is used to allow editing of the content via a simple CMS web interface.

### AWS

is used to host the website. Since it is a static website any CDN provider can be used in place here. Since forestry integrates very nicely with AWS (yes, it 2 clicks and adding your Bucket, Access Key and Secret 😲) and because i am a AWS fan I decided to use this.