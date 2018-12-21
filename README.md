# Nginx Configuration As Load Balancer
Here I will demoing how to use Nginx as load balancer 
## Instalation
Demo for nginx installation and configuration as load balancer
Lets start with setting up Nginx with your local system, following commands shoutl download and install nginx on your machine
```
brew update
brew install nginx
```
After successfull installation, run the Nginx
```
sudo nginx
```
It uses port 8080, open browser and see if its works http://localhost:8080 if this wokrs then you are done with installatoion.
use following if you want to stop it
```
sudo nginx -s stop
```
## Nginx as Load Balancer
First step would be add host entry in your host file. Let's take the example we want to serve local.testservice.com from local set of service instances. To add host entry open loca host file 
```
vi sudo vim /private/etc/hosts
```
and Below entry
```
127.0.0.1 local.testservice.com
```
Now next step is to setup nginx.conf, you can find nginx.conf at location 
```
/usr/local/etc/nginx/nginx.conf
```
if you open this file it looks like 
```
http {
  # ... ...
  # ... ... nginx stuff
  # ... ...
  
  # include all server conf files
  include servers/*;
}
```
as you at last it says that, its include all configuraiton files which are under folder "servers", so lets create separate configuration file under servers directory for out service
```
sudo vim /usr/local/etc/nginx/servers/myLocalTestService.conf
```
And below configuratio in this file, considering you have started service instances are avialble on ports 7979,8989. 
```
server{
	listen	80;
	server_name  local.testservice.com;

	location / {
		proxy_pass http://backend;
	}
}

upstream backend {
    server localhost:7979;
    server localhost:8989;
}
```
Once all the configuration is done you have to restart/reload the nginx server
```
sudo nginx reload
```
Now, whenever your hitting http://local.testservice.com on local machine it will get server from two server instances http://localhost:8989 and http://localhost:7979
