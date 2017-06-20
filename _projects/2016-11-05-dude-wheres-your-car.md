---
layout:     post
title:      "Dude where's your car?"
date:       2016-11-05
categories: projects
permalink:  /projects/dude-wheres-your-car
published:  true
---
## The Tech
This project was a single page app in Angular 2 and Google Maps front end, and .Net Core Web API back end using AWS SNS (Simple Notification Service) for text messaging between the service technician and the customer. This web app was hosted on AWS EC2.

## The Problem
The technician has arrived at the location of the vehicle to perform service, which was collected prior to this scope. They notice it is a giant parking lot and does not have enough information to find the vehicle quickly. So they press a button in the existing technician mobile app to send a text message to the customer asking them to narrow the location and description a bit. The message is generated from within the app so the tech does not specify the message.

## The Solution
The customer receives a text message with a link asking them to locate specifically where the vehicle is. When the link is clicked they are taken to a responsive web app presented below.

![Image](/assets/images/posts/dude-wheres-your-car-2.png)

If the vehicle is in an entirely different location - maybe they had to move it somewhere else or ended up staying home but forgot to notify the company - they have the option to click the link below the map and type in a different address.

![Image](/assets/images/posts/dude-wheres-your-car-3.png)

After the point on the map is shared (text message sent to tech), optional extra info is requested to help the technician find the vehicle. If this is shared, the tech will receive a second text message.

![Image](/assets/images/posts/dude-wheres-your-car-4.png)
![Image](/assets/images/posts/dude-wheres-your-car-5.png)
![Image](/assets/images/posts/dude-wheres-your-car-6.png)
