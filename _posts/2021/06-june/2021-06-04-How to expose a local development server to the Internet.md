---
title: 'How to expose a local development server to the Internet'
categories: webdev
---

As developers, we often need to share our work in progress with colleagues or clients who may not have access to our local development environment. That's where NGROK comes into play.

NGROK is a brilliant tool that allows you to expose your local server to the internet, thereby facilitating real-time updates and troubleshooting. Here's a step-by-step guide on how to utilize this software effectively.

To begin with, navigate to the NGROK website and download the appropriate version for your operating system. Once downloaded, extract the NGROK executable file to your preferred directory.

Before you can use NGROK, you need to sign up for a free account on the NGROK website. After registration, you'll be provided an auth token. This token will be used to authenticate your NGROK instance. You can do this by running the command ./ngrok authtoken YOUR_AUTH_TOKEN in your terminal.

Now, it's time to expose your local development server. Suppose your application is running locally on port 8080. To make this server accessible over the internet, execute ./ngrok http 8080 in your terminal. Within moments, NGROK will provide you with a unique URL that points directly to your local server.

The beauty of NGROK is the ease with which you can share this URL with anyone, enabling them to access your application as if it were hosted on a public server. Furthermore, NGROK also provides a beautiful interface at http://localhost:4040 where you can inspect all HTTP traffic for your tunnels.