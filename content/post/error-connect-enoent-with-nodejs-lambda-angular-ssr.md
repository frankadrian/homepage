+++
author = "Frank Adrian"
comments = false
date = "2019-05-21T22:00:00+00:00"
tags = ["aws-lambda", "nodejs", "angular-ssr"]
title = "AWS Lambda Error: connect ENOENT /tmp/server-*.sock with nodejs lambda angular ssr"

+++
## Background

We have a SSR Angular application hosted on AWS. The Lambda function renders the requested page in front of an Api Gateway. We use [serverless](https://serverless.com/) and an nodejs express server to render the requested page or resource.

This error kept showing up when accessing our lambda serverless angular build from multiple regions simultaneously:

    { Error: connect ENOENT /tmp/server-q2r7kv33bik.sock
    	at Object._errnoException (util.js:1022:11)
    	at _exceptionWithHostPort (util.js:1044:20)
    	at PipeConnectWrap.afterConnect [as oncomplete] (net.js:1198:14)
    	code: 'ENOENT',
    	errno: 'ENOENT',
    	syscall: 'connect',
    	address: '/tmp/server-q2r7kv33bik.sock' 
     }

The Api Gateway simply returned an 502 response code.

![](/uploads/502-error.png)

## The Solution

was not very obvious at first, but once we found the problem it was a quick fix:  
We are heavily relying on localStorage in our Angular Application and so had to mock this part in order to enable Server Side Rendering of our webpage. For this purpose exists this awesome [node-localstorage](https://www.npmjs.com/package/node-localstorage) package. What this does is create a file on your local filesystem and use this file as a localStorage store.

Here we specified /tmp as the location to write this store:

    let localStorage = new LocalStorage('/tmp');

Because this script runs as a NodeJS Lambda function, /tmp is the temp directory of this function which happens to be shared across multiple function executions that don't require a cold start. 

This is the reason we only experienced this Error when multiple clients requested our webpage at more of less the same time, As for the second invocation Lambda shared the /tmp directory which was now only a file containing our LocalStorage data. And so the server could not connect to /tmp/server-q2r7kv33bik.sock anymore.

So changing our LocalStorage initialisation to something like:

    let localStorage = new LocalStorage('/tmp/localStorage');

did the trick and we no longer experienced the 502 errors.
