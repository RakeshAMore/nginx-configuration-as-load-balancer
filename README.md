# Nginx Configuration As Load Balancer
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
Lets setup nginx.conf, you can find nginx.conf at location 
```
/usr/local/etc/nginx/nginx.conf
```
