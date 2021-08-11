# learner
https://ajessh.signin.aws.amazon.com/console

Created AWS learner profile for user "Ajessh" under IAM module
Created a EC2 instance in AWS
Connect EC2 instance using SSH

Install yum-config-manager to manage package
$ sudo yum install -y yum-utils

Use yum-config-manager to add the official HashiCorp Linux repository.
$ sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo

########  Install terraform and create main.tf for EC2 instance creation ########
$ sudo yum -y install terraform

$ create aws configure

create a teraform file main.tf
cat main.tf 
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.27"
    }
  }

  required_version = ">= 0.14.9"
}

provider "aws" {
  profile = "default"
  region  = "eu-west-2"
}

resource "aws_instance" "sample_server" {
  ami           = "ami-0d26eb3972b7f8c96"
  instance_type = "t2.micro"

  tags = {
    Name = "SampleServerInstance"
  }
}

$ terraform init

$ terraform fmt

$ terraform validate

$ terraform apply

$ terraform show

########  EC2 Instance created succesfully ########


###### Add a new user with sudo access ######
$ sudo adduser ajess
$ sudo passwd username

$ sudo usermod -aG wheel username

#disable root access
$ sudo vim /etc/passwd

root:x:0:0:root:/root:/bin/bash
to
root:x:0:0:root:/root:/sbin/nologin

##### Shell script for mointoring free disk space ####
#!/bin/sh
df / >> /var/log/freespace/df.log | date >> /var/log/freespace/df.lo

created folder /var/log/freespace
and a file df.log

created a .sh file mointer_df.sh and append the code inside

run the sh and check whether the log is generated
$ bash mointer_df.sh

###### Cron job creation ######
$ crontab -e
1-59 * * * * bash /var/script/monitor_df.sh --report /etc/cron.hourly
$ crontab -l

###### Hourly Configuration #####
$ cp /etc/cron.daily/logrotate   /etc/cron.hourly/

#/usr/sbin/logrotate /etc/logrotate.conf
/usr/sbin/logrotate  /etc/logrotate.d/learn_df.config

###### learn_df.config file creation for logrotation ######
/var/log/freespace/*.log {
hourly
rotate 10
copytruncate
compress
delaycompress
}

###### Netdata installation ######
$ bash <(curl -Ss https://my-netdata.io/kickstart.sh)

$ systemctl status netdata

###### install nginx ######
$ sudo apt install nginx

$ systemctl enable nginx
$ service nginx status

##### created a sample page in the below path #####
$ /var/script/ng_sample_webpage/index.html

##### changed the nginx config to display the webpage created #####
/etc/nginx/nginx.conf
root     /var/script/ng_sample_webpage;

### curl output ###
curl -lv http://localhost/index.html
*   Trying 127.0.0.1:80...
* Connected to localhost (127.0.0.1) port 80 (#0)
> GET /index.html HTTP/1.1
> Host: localhost
> User-Agent: curl/7.76.1
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Server: nginx/1.20.0
< Date: Wed, 11 Aug 2021 20:45:48 GMT
< Content-Type: text/html
< Content-Length: 217
< Last-Modified: Wed, 11 Aug 2021 13:31:15 GMT
< Connection: keep-alive
< ETag: "6113d123-d9"
< Accept-Ranges: bytes
< 
<!doctype html>
<html>
        <head>
              <meta charset="utf-8">
              <title>Hello, SKY!</title>
        </head>
        
<body>
       <h1>Hello, Sky</>          
     
</body>
</html>
* Connection #0 to host localhost left intact
  
  
  
  ######## EC2 Instance AMI image ######
  AMI ID   =  ami-008d565c72ed6b4a6
  AMI Name = aws-learner-image

