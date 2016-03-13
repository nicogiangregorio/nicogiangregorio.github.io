---
author: Nico Giangregorio
layout: post
title: "Fast local development with Docker"
date: 2016-03-13 22:10
comments: true
tags:
- docker
- zabbix
---

Recently I've been involved in a feasibility study for a project about monitoring of multiple large data center.  
Avoiding further details, I identified a useful tool to kick off a custom solution development: <a href="http://www.zabbix.org/" target="_blank">Zabbix</a>.

The first problem is: I never used Zabbix and I am not sure it is the right tool for the purpose.  
The second problem is even worst: in order to play with Zabbix I need at least of nginx, php, mybash, java, CentOS etc. Hence a complete environment I do not have right now.

So what I need is a **quick setup of Zabbix on my local machine** and being able to evaluate Zabbix as soon as possible.

How to solve this problem? EASY!
With **<a href="https://www.docker.com/" target="_blank">Docker</a>**!

Precondition: I have a full running docker-machine on my laptop, with Docker toolbox.

First thing to check: There is an entry in Docker Hub for Zabbix? <a href="https://hub.docker.com/r/zabbix/zabbix-3.0/" target="_blank">Yes</a>!  
Second step, let's check if there is a .yml file read to launch. Well, if you read the doc of Zabbix's DockerHub entry, it is quite easy.  
You can find it here: <a href="https://github.com/zabbix/zabbix-community-docker" target="_blank">Yes</a>! Zabbix-docker-github-repo

So the full instructions are the following:

Start your docker console (Docker Quickstart Terminal on wondows hosts).
{% highlight bash%}
mkdir zabbix-nico
cd zabbix-nico
{% endhighlight %}
Clone the zabbix-docker repo:
{% highlight bash%} 
git clone https://github.com/zabbix/zabbix-community-docker.git
cd Dockerfile/zabbix-3.0
{% endhighlight %}
Build your image
{% highlight bash%} 
docker build -t zabbix_nico .
{% endhighlight %}
where *zabbix_nico* is the name of the docker image.

Start with docker compose:
{% highlight bash%} 
docker-compose.exe up
{% endhighlight %}
That's all! Your zabbix local environment is up & runnnig.
Oh well, you would like to see if it is working.
Ok, let's check the ip address of your machine
{% highlight bash%} 
docker-machine ip default
192.168.99.100
{% endhighlight %}
*default* is the name of my machine.
now point your browser to: [http://192.168.99.100/](http://192.168.99.100/) et voilà!  

![Zabbix]({{ site.url }}/images/zabbix.png)

In short: this is my better experience with docker: rapid prototyping and a ready-to-go dev environment.