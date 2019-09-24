# nginx-aws-box
Nginx AWS EC2 box

# Purpose
This repository contains the minimal code and instructions required to create an **AWS EC2** instance box with **Nginx** web server.

To learn more about the mentioned above tools and technologies -  please check section [Technologies near the end of the README](#technologies)

# Instructions

- To create image we are going to provision instance in Amazon EC2 service. When building, you'll pass in **aws_access_key** and **aws_secret_key** as user variables, keeping your secret keys out of the template. You can create security credentials on [this page](https://console.aws.amazon.com/iam/home?#security_credential). An example IAM policy document can be found in the [Amazon EC2 builder docs](https://www.packer.io/docs/builders/amazon.html). **NEVER** save your credentials directly in the template file or any other repo parts.
- To download the copy of the code (*clone* in Git terminology) - go to the location of your choice (normally some place in home folder) and run in terminal:
 ```
 git clone https://github.com/Galser/nginx-aws-box.git
 ```
 *in case you are using alternative Git Client - please follow appropriate instruction for it and download(*clone*) [this repo](https://github.com/Galser/nginx-aws-box.git).*

- Previous step should create the folder that contains a copy of repository. The default name is going to be the same as the name of repository e.g. `nginx-aws-box`. Locate and open it.
 ```
 cd nginx-aws-box
 ```
- Now to create the AWS EC2 box with Nginx we are going to use Packer and [template](nginx-aws-template.json) with [provision scripts](scripts) provided in this repo.
*Note: It is going to take some time, as Packer need to start instnce, wait for it to be up and running, provision and then pack everything into an AMI - format of images used in Amazon EC2*

To simplify the process we use the credentials in the command line. However, it is potentially insecure. See official  documentation for [other ways to specify Amazon credentials](https://www.packer.io/docs/builders/amazon.html#specifying-amazon-credentials).
 ```
 packer build \
    -var 'aws_access_key=YOUR ACCESS KEY' \
    -var 'aws_secret_key=YOUR SECRET KEY' \ 
    nginx-aws-template.json
 ```
 You should see these lines at the start of the output :
 ```
 amazon-ebs output will be in this color.

 ==> amazon-ebs: Prevalidating AMI Name: nginx-aws 1569332194
     amazon-ebs: Found Image ID: ami-04763b3055de4860b
 ==> amazon-ebs: Creating temporary keypair: packer_5d8a1be2-2948-0eed-5676-ce819d11def2
 ==> amazon-ebs: Creating temporary security group for this instance: packer_5d8a1be6-c9fc-084f-5a01-94d65bebce1d
 ==> amazon-ebs: Authorizing access to port 22 from [0.0.0.0/0] in the temporary security groups...
 ==> amazon-ebs: Launching a source AWS instance...
 ```
>>> we skipping several pages of output here, and jumping to the end of it

And in the case of successful process completion you would see these *last lines* :
 ```
 ==> amazon-ebs: Creating AMI nginx-aws 1569332194 from instance i-0c1a055e58ca2f7ad
     amazon-ebs: AMI: ami-05109863b0a1a6a3e
 ==> amazon-ebs: Waiting for AMI to become ready...
 ==> amazon-ebs: Terminating the source AWS instance...
 ==> amazon-ebs: Cleaning up any extra volumes...
 ==> amazon-ebs: No volumes to clean up, skipping
 ==> amazon-ebs: Deleting temporary security group...
 ==> amazon-ebs: Deleting temporary keypair...
 Build 'amazon-ebs' finished.

 ==> Builds finished. The artifacts of successful builds are:
 --> amazon-ebs: AMIs were created:
 us-east-1: ami-05109863b0a1a6a3e
 ```
Here - at the end of the run Packer outputs the artifacts that were created as part of the build. Artifacts are the results of a build, and typically represent an ID (such as in the case of an AMI) or a set of files (such as for a VMware virtual machine). In this example, we only have a single artifact: the AMI in us-east-1 that was created with ID  : **ami-05109863b0a1a6a3e** 

This AMI is ready to use. If you wanted you could go and launch this AMI right now and it would work great.

  > Note: Your AMI ID will surely be different than the one above. If you try to launch the one in the example output above, you will get an error. If you want to try to launch your AMI, get the ID from the **your** Packer output.

This ends up instruction block, thank you. 



# Technologies

1. **To download the content of this repository** you will need **git command-line tools**(recommended) or **Git UI Client**. To install official command-line Git tools please [find here instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for various operating systems. 
2. **This box for virtualization** uses **AWS EC2** - Amazon Elastic Compute Cloud (Amazon EC2 for short) - a web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers. You can read in details and create a free try-out account if you don't have one here :  [Amazon EC2 main page](https://aws.amazon.com/ec2/) 
3. **For creating AWS EC2 image** we need **Packer** - an open-source tool for creating identical machine images for multiple platforms from a single source configuration.  You can [download binaries for your platform here](https://www.packer.io/downloads.html)  and then [follow this installation instruction](https://www.packer.io/intro/getting-started/install.html#precompiled-binaries).  
4. **Nginx stands apart - as it will be downloaded and installed automatically during the provision.** Nginx is an open source HTTP Web server and reverse proxy server.In addition to offering HTTP server capabilities, Nginx can also operate as an IMAP/POP3 mail proxy server as well as function as a load balancer and HTTP cache server. You can get more information about it check [official website here](https://www.nginx.com)  

# TODO 


# DONE

- [x] make initial README
- [x] prepare AWS creds in env vars
- [x] update instructions for the security and AWS credentials approach
- [X] create initial Packer template with default bare minimal system
- [X] add Nginx provision into template
- [x] update instructions
