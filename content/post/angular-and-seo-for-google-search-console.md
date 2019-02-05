+++
author = "Frank Adrian"
comments = true
cover = ""
date = "2019-02-04T23:00:00+00:00"
tags = ["angular", "web-development"]
title = "Angular and SEO for google search console"

+++
# It is 2019 and Google is able to index website build using Javascript frameworks like React, Angular or AngularJS.

Recently I got the following preview for a website which was build using Angular 7 and google show this as a preview: (blank screen for "This is how Googlebot saw the page:" and "This is how a visitor to your website would have seen the page:")

![Google search console rendering preview](/uploads/Screenshot 2019-02-05 at 14.32.43.png "Google search console rendering preview")

This was not what I signed up for. As i knew Google is able to crawl Angular 2+ websites because i have seen it for a previous project I built.

After hours of searching and debugging I think I found the trivial reason for why the page showed as blank.

It turns out google crawler uses a rather old version of the chrome rendering engine which [does not support ES6](https://developers.google.com/search/docs/guides/rendering), and it requires several polyfills for Angular pages to get rendered.

It is even noted in the polyfills.ts (if you use the angular cli) that the following polyfills need to be enabled for Googles Search Bot :)

![angular cli polyfills.ts](/uploads/Screenshot 2019-02-05 at 14.50.17.png "angular cli polyfills.ts")

After enabling these, the page was immediately rendered by the Google Search Console.  
![Google Search Console rendered results](/uploads/Screenshot 2019-02-05 at 14.49.47.png "Google Search Console rendered results")

Hopefully this can help you if you want an Angular Webpage to be indexed by Google SearchBot.