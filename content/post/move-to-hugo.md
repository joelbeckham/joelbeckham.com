+++
date = "2015-12-17T20:58:29-07:00"
draft = true
title = "move to hugo"

+++

#1. Create S3 Bucket
Create a new bucket with name _exactly_ matching the domain under which you want to host it.

Add a bucket policy:

    {
        "Version": "2012-10-17",
        "Statement": [{
            "Sid": "site-readers",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::preview.joelbeckham.com/*"
        }]
    }

Under Static Site Hosting, select "Enable website hosting".
Set index document to _index.html_
Set Error Document to _404.html_

Copy the endpoint it gives you.
In your DNS, create a new CNAME record and point it to the S3 endpoint.

Created another bucket without the www.
Under Static Site Hosting, select "Redirect all requests to another host name"
Set "Redirect all requests to" to _www.joelbeckham.com_

#2. Create IAM user for deployment


#2 Create new Github repo.


In the project root, make a file called _gitignore.txt_ (we'll rename later)
From the command line type rename gititnore.txt .gitignore


#3 Signup for Travis

#4 Install Travis CLI
This is needed to encrypt AWS keys in the Travis config.

Install the rubygem:

    gem install travis

Received this error:

    ERROR:  While executing gem ... (Gem::RemoteFetcher::FetchError) bad response Not Found 404 (https://rubygems.global.ssl.fastly.net/quick/Marshal.4.8/pry-0.9.12.6-x86-mingw32.gemspec.rz)

Which turns out to be a known [bug](https://github.com/rubygems/rubygems/issues/1120). Downgrading to rubygems-2.4.4 is the workaround for now:

    gem update --system 2.4.4

Retry install

    gem install travis

It worked!

    12 gems installed

#5 Create .travis.yml
**Make sure you don't accidentally commit your raw AWS credentials to travis.yml. They recommend you encrypt them first. You can do this with the travis cli.**

From the command line

    travis init go
       
Got this error
 
    No such file or directory - git config --get travis.slug
    
Means git is not available in PATH. Install git:

    https://git-for-windows.github.io/

Close and reopen terminal

    travis init go
    
Then 

    travis setup s3
    
It'll ask you a series of questions to populate .travis.yml for you. A couple questions worth noting:
 * For _"Local project directory to upload"_ enter _public_
 * For _"S3 ACL Settings"_ enter _public_read_
 
#6 Edit .travis.yml

Under the language section:
    
    language: go
    go:
    - '1.0'
    - '1.3'
    
Remove version "- '1.0'"

After the go: section but before the deploy: section add:

    sudo: required
    install:
      - go get github.com/spf13/hugo
    script: hugo --theme="hyde" --destination="public" -v

    
Also, anywhere in the deploy section add:

      skip_cleanup: true
	  
Without this, Travis deletes everything before the deploy step and you won't be able to deploy.

#6 Get Hugo and Test


#7 Export From Wordpress
Install hugo exporter




# Documentation
* Travis S3: https://docs.travis-ci.com/user/deployment/s3



# TODO
.gitignore public
Remove public from github