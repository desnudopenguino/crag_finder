# Rock Finder
A web app designed for helping rock climbers identify and locate potential outdoor climbing areas based on geographic and geologic data.

# Installation & Notes
This section describes the installation process so that installation can be repeated. These are the steps taken from guides/docs all over the internet consolidated into one guide to ensure repeatability, and remove the need to go hunt down directions/configs in the future.

The Rails App name is myapp.example.com.

The initial installation/version will be running on a Debian VM in VirtualBox.

1 Create your environment, make sure things are up to date: sudo apt-get update

2 Install NGINX (web server): sudo apt-get install nginx

3 Install PostgreSQL: sudo apt-get install postgresql

4 Install Ruby on Rails:

 4.1 Install Ruby and other useful bits: sudo apt-get install ruby rdoc ruby-dev libopenssl-ruby rubygems
 
 4.2 Install fastthread: sudo gem install fastthread
 
 4.3 Instal rails: sudo gem install rails
 
 4.4 Add rails to your PATH: PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/var/lib/gems/VERSION/bin" # (VERSION is the version of Ruby being used)
 
 4.5 Create Rails app: 
 
  4.5.1 cd /var/www
  
  4.5.2 rails new myapp.example.com
  
  4.5.3 At this point, the app crashes due to a missing javaScript runtime environment, so add one
  
   4.5.3.1 Edit the Gemfile, adding the following lines to the end of the file:
   
   gem 'execjs'
   
   gem 'therubyracer'
  
  4.5.4 Bundle the gems for the app: bundle install

5 Configure Rails and NGINX to work well together:

 5.1 Get the gem for the Rails HTTP server of choice (Thin used here): sudo gem install thin 

 5.2 Install the Rails HTTP server: sudo thin install
 
 5.3 Set Thin server defaults: sudo /usr/sbin/update-rc.d -f thin defaults
 
 5.4 Create default Thin config file: sudo thin config -C /etc/thin/myapp.example.com -c /var/www/myapp.example.com --servers 3 -e development # (or: -e production for caching, etc.)
 
 5.5 Add Thin to the Gemfile: 
 
 gem 'thin'

6 Restart/start the server daemons:

 6.1 Start the rails service (cd into /var/www/myapp.example.com): rails s
 
 6.2 Restart NGINX: sudo /etc/init.d/nginx reload

# Useful Links
NGINX Beginner's Guide: http://nginx.org/en/docs/beginners_guide.html

Running Ruby on Rails on NGINX: http://kvz.io/blog/2010/09/21/ruby-with-nginx-on-ubuntu-lucid/
