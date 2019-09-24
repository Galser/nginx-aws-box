# nginx-aws-box
Nginx AWS EC2 box

# Purpose
This repository contains the minimal code and instructions ot create an AWS EC2 instance box with Nginx web server.

To learn more about the mentioned tools and technologies -  please check section [Technologies near the end of the README](technologies)

# Instructions

- To create image we are going to provision instance in Amazon EC2 service. When building, you'll pass in **aws_access_key** and **aws_secret_key** as user variables, keeping your secret keys out of the template. You can create security credentials on [this page](https://console.aws.amazon.com/iam/home?#security_credential). An example IAM policy document can be found in the [Amazon EC2 builder docs](https://www.packer.io/docs/builders/amazon.html). **NEVER** save your credentials directly in the template file or any other repo parts.
- 

# Technologies

1. **To download the content of this repository** you will need **git command-line tools**(recommended) or **Git UI Client**. To install official command-line Git tools please [find here instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for various operating systems. 
2. **This box for virtualization** uses **AWS EC2** - Amazon Elastic Compute Cloud (Amazon EC2 for short) - a web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers. You can read in details and create a free try-out account if you don't have one here :  [Amazone EC2 main page](https://aws.amazon.com/ec2/) 
3. **For creating base box image** from scratch we need **Packer** - an open-source tool for creating identical machine images for multiple platforms from a single source configuration.  You can [download binaries for your platform here](https://www.packer.io/downloads.html)  and then [follow this installation instruction](https://www.packer.io/intro/getting-started/install.html#precompiled-binaries).  In our case Packer is going to take care of installing OS into VM, communicating with it, doing basic provision and preparing for us packed Vagrant box, ready to use.

4. **Nginx stands apart - as it will be downloaded and installed automatically during the provision.** Nginx is an open source HTTP Web server and reverse proxy server.In addition to offering HTTP server capabilities, Nginx can also operate as an IMAP/POP3 mail proxy server as well as function as a load balancer and HTTP cache server. You can get more information about it check [offical website here](https://www.nginx.com)  

# TODO 

- [ ] add Nginx provision into template
- [ ] update instruction

# DONE

- [x] make initial README
- [x] prepare AWS creds in env vars
- [x] update instructions for the security and AWS credentials approach
- [X] create initial Packer template with default bare minimal system
