---
title: Debugging on remote server with Xdebug
date: 2025-04-01
tags:
    - php
categories:
    - EN
---



Sometimes it may be useful to run Xdebug on the server where the PHP code is being executed. Here is how to set it up.
<!-- more --> 

Xdebug, even if disabled, adds some performance footprint, so it's not recommended to have it installed on production servers. Mostly you use Xdebug on your local computer. But sometimes there are situations when you need to debug the code execution in the certain environment, which can't be modeled locally. For example, you have a bug, that is not reproducible with local database. Or you need to inspect the specific flow, which works only on production. In such cases it may be useful to temporarily install Xdebug on the remote servers, where your code is executed. Still, it's preferably to do it on the dedicated QA environment, not in production.

Installing Xdebug on a remote server probably doesn't differ a lot from installing it locally. The trick is in getting Xdebug to connect to your IDE, which listens on local computer. For this purpose we need our local computer to be accessible from the Internet. There are many ways to achieve this, using a tool called Ngrok is the most popular solution. But Ngrok is not free. Still, there are lots of alternatives, cheaper or even partially free. One of them is Expose.dev, which provides free plan and which I've used a lot for presenting apps, running locally, to the internet.

At first, I tried to use Expose.dev to expose



