+++
author = "Frank Adrian"
comments = true
cover = "/uploads/how i build this website.png"
date = "2018-11-10T13:13:38+00:00"
tags = ["web development", "aws", "hugo"]
title = "How I build this website"

+++
This post outlines how I initially built this website, using a couple of services and open source projects, all in the cloud and (almost) completely for "free" (excluding the domain name (you could use github pages for free) and provided you stay in the [free tier](https://aws.amazon.com/free/?awsf.Free%20Tier%20Types=categories%23alwaysfree)).

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

## Piecing them together

### Create your custom website

install hugo and generate a new site

    brew install hugo
    
    hugo new site homepage

Install the theme as a submodule

    git submodule add https://github.com/laozhu/hugo-nuo themes/hugo-nuo

follow instructions here to configure an example site: [https://github.com/laozhu/hugo-nuo#getting-started](https://github.com/laozhu/hugo-nuo#getting-started "https://github.com/laozhu/hugo-nuo#getting-started")

commit all files (see example [.gitignore](https://github.com/frankadrian/homepage/blob/master/.gitignore)) and push to github

### Create content for your website

signup at forestry and import your github repository. This will create your project and allows you to directly change the contents on your website if you followed the instructions to create the example site.

### Setup hosting

I used this [aws cloudformation stack](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=my-static-site&templateURL=https%3a%2f%2fs3.amazonaws.com%2fforestryio-cf-templates%2fstatic-site-hosting%2fadvanced-route53-acm.yml) to create everything on the aws front. This requires you have a domain setup and validated on Route 53 with a Domain Zone setup.

### Setup Deployment

On forestry go to _Settings -> Deployment_ and enter your _user access key_ and _secret_ as well as the _S3 bucket_.

Go to _Settings -> General_ and make sure to switch _Deploy to github_ on

This automatically deploys your changes to S3 on every change you make in forestry (or the github repository) Pretty sweet if you ask me 🤓