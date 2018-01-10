---
layout: post
title:      "Making Your Localhost Publicly Available via SSH Tunneling"
date:       2018-01-10 22:48:22 +0000
permalink:  making_your_localhost_publicly_available_via_ssh_tunneling
---


**3rd Party Services Will Not Be Able to Find Your Local Application On Your Localhost**

In web development, running a local environment is often necessary to test code as it is being developed.  However, when developing against a webhook-based API, this presents a challenge as a HTTP callback using 'localhost' will not be able to find your 'localhost' address as it is only available to your local machine.

So how can we make a localhost publicly available so an application in development can provide a webhook to work with 3rd party services?

**Use an SSH Tunneling Service**

A common solution to this dilemma is to utilize secure shell (SSH) tunneling.  Using SSH on a public hosted box, it forwards requests on a specific port to your local machine.

For example, if you want a 3rd party service to be able to POST to your application's API on development upon a certain event, you can set up SSH tunneling so that callbacks can be made to a public url, which will be forwarded to a specific port on your local machine.

The easiest way to get started is some programs already available.  Some popular ones are:

* [Ngrok](http://www.ngrok.com)
* [Localtunnel.me](http://www.localtunnel.me)
* [Localhost.run](http://localhost.run)

With these services, set up is quite minimal and involves executing a few shell commands. In turn, they will return the public url after the tunneling service is established, and make your application's REST API routes available to 3rd party services.

**Tip**

When utilizing such services, obtaining and reusing a static, customized subdomain is ideal.  The reduces the need to change the public url on the webhook's service(s) everytime the SSH tunneling service is restarted.
