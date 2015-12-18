#1. Create S3 Bucket
Create a new bucket with name _exactly_ matching the domain under which you want to host it.

Add a bucket policy:

Enable static site hosting.
Copy the endpoint it gives you.
In your DNS, create a new CNAME record and point it to the S3 endpoint.

Created another bucket without the www.
Turned on redirection and pointed it to www.joelbeckham.com

#2. Create IAM user for deployment


#2 Create new Github repo.
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


#5 Create Travis.yaml
**Make sure you don't accidentally commit your raw AWS credentials to travis.yml. They recommend you encrypt them first. You can do this with the travis cli.**

#6 Get Hugo and Test


#7 Export From Wordpress
Install hugo exporter




