+++
author = "Frank Adrian"
comments = true
cover = ""
date = "2019-01-30T23:00:00+00:00"
tags = ["web-development", "aws", "lambda", "sitemap-generator"]
title = "nodejs lambda sitemap generator "

+++
# Lambda function to generate sitemap from mysql

[This](https://github.com/frankadrian/lambda-sitemap-generator) is a simple example of how you can use nodejs to generate a sitemap for your Angular application. [Since Google can now index Angular application](/post/angular-and-seo-for-google-search-console/) a sitemap helps the crawlers to find all your pages.

I wanted to connect directly to our database to generate urls for dynamic pages. This was easily setup using our existing VPC and running the function inside of the VPC.