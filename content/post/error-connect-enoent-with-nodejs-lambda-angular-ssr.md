+++
author = "Frank Adrian"
comments = false
cover = ""
date = "2019-05-21T22:00:00+00:00"
tags = ["aws-lambda", "nodejs", "angular-ssr"]
title = "Error: connect ENOENT with nodejs lambda angular ssr"

+++
# AWS Lambda Error: connect ENOENT /tmp/server-*.sock

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

was to return a promise from the `awsServerlessExpress.proxy()` call in the lambda handler and declare the function as async:

    module.exports.universal = async (event, context) => {
      return awsServerlessExpress.proxy(serverProxy, event, context, 'PROMISE').promise;
    };

Also make sure you are using at least version 8 of nodejs to support async/await.