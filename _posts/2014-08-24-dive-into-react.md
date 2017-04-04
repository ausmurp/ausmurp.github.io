---
layout:     post-hero
title:      "Dive into React"
date:       2015-08-24
categories: react
cover:      http://createdwithflair.com/wp-content/uploads/2016/03/react.png
permalink:  /blog/dive-into-react
---
React. Is. Amazing.

### What is Vagrant


### Getting started



### Basic Vagrant manage


### Provisioners

The most basic provisioner is **Shell script**. If you need more provisioning power (probably you do) Vagrant has support for multiple IT automation tools such as [Chef](http://www.getchef.com/chef/), [Puppet](http://puppetlabs.com/), or [Ansible](http://www.ansible.com/home). To use a provisioner you just have to add [configuration](http://docs.vagrantup.com/v2/provisioning/index.html) to your `VagrantFile`.

It's convenient to mention here a tool that is moving mountains these days: [Docker](http://www.docker.io). It's an open-source project to easily create lightweight, portable, self-sufficient containers from any application. If you know about this tool, you shouldn't see it as a Vagrant "killer". In fact I think that combining both is a win since Vagrant 1.5 can integrate with Docker using it as a provisioner.  

Configuration through automation tools is a very wide topic, and each tool has its own documentation, so for teaching purposes we are going to check just an example with Shell. We will write a script to install `nginx` and let you do the rest with other tools. Add to the configuration block, inside the VagrantFile, this line:

```ruby
config.vm.provision "shell", path: "script.sh"
```

This is telling Vagrant that at the provisioning moment we want to use shell  to run `script.sh`. Let's, create that `script.sh` file in the same folder as your `VagrantFile` containing:

```bash
echo “Running installation of nginx”
sudo apt-get update
sudo apt-get -y install nginx
sudo service nginx start
```

Provisioning is made when `vagrant up` is run. In order to run only the provisioning tools you can use the command `vagrant provision`. Let's do it and you’ll see how the commands in the script are executed. The cool thing about this if that if we document all the pieces of software and its configuration through provision tools, we can destroy the machine and run Vagrant up, then we have everything ready to work. Try it out and go to `http://localhost:8080` in your host again, you'll see everything working again.

With powerful tools such as Chef, we can replicate our environment, or even recycle our scripts to use them in production and have the very same environment in production and development for testing purposes. Cool, isn't it?

### The Cloud

Recently, Vagrant 1.5 was released with new and great features. With this new version, Vagrant has a Cloud for sharing, discovering and creating Vagrant environments through boxes. Did you heard about [localtunnel](http://localtunnel.me/)? Well, now the cloud is giving you another cool feature: sharing your running environment with anyone connected to Internet. Pretty much the same that localtunnel does.

To use this feature, sign up in [Vagrant Cloud](https://vagrantcloud.com/) and then login through the command line with `vagrant login`. Then, with your machine running and nginx installed (just for demo purposes), run `vagrant share`. A random URL will be generated to share with anyone. Vagrant will search for HTTP servers listening in your machine and map them to the URL given. In our example case, since nginx is listening on port 80, any request made to the share url in port 80 is going to be redirected to port 80 inside your machine. This is a great feature to share your development work with others. You can check a video [demo here](http://vimeo.com/87525972).

But best thing is that you can even let others to connect to your machine using SSH! When you are running `vagrant share`, use `--ssh` flag. Vagrant will ask you for a password and give you instructions to connect to your machine from outside running `vagrant connect --ssh <random-name-given>`. View a [demo here](http://vimeo.com/87525810).

You can also run `vagrant connect <random-name-given>` without ssh option and vagrant will create a tiny virtual machine to handle routing between you and the remote Vagrant environment. When you run it, an IP address will be given. You can directly ssh to that IP and you'll be inside the machine. You have a [demo here](http://vimeo.com/87590529).

### Conclusion

Vagrant let you create development environments that are portable, lightweight and easy to use. You can share the environments using Vagrant Cloud or giving the configuration files with a provisioning system. You can now have your whole team working on the very same environment, even replicate your production environment too, deleting all the problems mentioned above! Here you have some links for further reading:

- [Vagrant: Up and Running](http://shop.oreilly.com/product/0636920026358.do) by Mitchell Hashimoto, creator of Vagrant.
- [Vagrant Cookbook](https://leanpub.com/vagrantcookbook) by Erika Heidi.
- [Vagrant Railscast](http://railscasts.com/episodes/292-virtual-machines-with-vagrant?view=asciicast) by Ryan Bates

Nice hacking time!
