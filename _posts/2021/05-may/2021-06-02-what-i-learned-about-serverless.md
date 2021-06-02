---
title: What I learned about serverless while trying to write free online converter?
categories: cloud
---

Some time ago I found C++ binary to convert files from STL to STP (STL is basically raster for 3D models, while STP is Vector).


## What was before cloud?

When I initially created wrapped for C++ binary I wrote Nodejs code that based on Expressjs and some Dockerfiles would build me a container which I could deploy anywhere.

For some time I had a good AppService plan where I kept my container and it worked flawlessly. But that didn't last long (about a year).

When I was faced with finding new home for this container, I thought I will host it on my local NAS. I don't use it that much so it seemed like a good idea. But it wasn't. Models uploaded would often consume a lot of ram, also this container didn't respect any queues or nothing so sometimes people would spawn many instances of converter and freeze my server eating up whole ram and swap space.

I rewrote the script to convert only one model at the time and that worked somehow up till not - but nothing amazing of experience for my as host and for users.

I want to improve that with some serverless cheap compute power!

## Azure Functions
Firstly I wanted to convert into Azure functions, I have bigger experience working with Microsoft's Cloud so that's where I started.

First of all it annoyed me that I needed to install a lot of CLI tools to create simple one javascript file function.

When I managed to create some kind of HelloWorld HttpTrigger and publish it to Azure fuctions, I was set up.

On the plus side of local CLI Tools, I could easily test my code locally and understand what is happening.

I managed to rewrite whole thing quite quickly althought typical for these problems it took me a while to find a piece of code that would parse multipart POST request into files, but with Busboy npm package I managed to do that.

The code worked, but when I tried converting bigger models I stumbled upon a problem that azure was killing my binary process.

In logs I found: `exit_code: 137`. Quick google search pointed me into answer: memory exceeded.

Turns out that consumption plan for Azure Fuctions only allows for 3,5GB of Ram. Which ususally would be plenty, but not for my big 3d models.

Well maybe AWS Lambda will help with that?


## AWS Lambda
Initial start was much easier for AWS Lambda, I opened my AWS Console webpage and started creating Lambda.

Firstly it didn't require as much parameters off start like Azure did.

Very quickly I was in front of text editor on web page that showed me my javascript file for function. I was happy, but that happiness didn't last long.

I noticed that I need API Gateway to make this function a "HttpTrigger" like I did it in Azure. This immediately sprung up questions if API Gateway will cost me fortune?

I checked quickly and pricing didn't seem very expensive so I went and created one.

Basing on experiences when converting my expressjs code to Azure Fuctions I was thinking that it will be easy to convert Azure Functions code to AWS Lambda.

There were some gotchas about how request is passed and how enviroment is working but I managed to quickly convert function's arguments.

What I spent most time fighitng with is async response and spawning child process. It was a big struggle but after some time of fighting with responses and googling I managed to get successful conversion.

I needed to use synchronized, callback style code for AWS to finally process this.

I configured my Lambda to have 6144MB RAM limit and I put my big test 3d model to see if we don't have memory issues like Azure does (3,5GB ram limit).

It didn't work! Why? Well there is this specific AWS Lambda limit on responses. You can't exceed 6MB. If You have bigger files, You need to upload them into S3 and redirect user to that.

That architectural decision complicates whole project because it requires me to pay additionaly for operations on S3, on storage on S3, and also making sure to remove files from S3 after some time (when?).

I turned off my AWS Lambda and currently I'm still hosting my free converter on Azure.

I need to research other clouds and see if they offer something that will work for me?
