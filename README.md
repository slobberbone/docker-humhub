# HumHub
[HumHub](https://www.humhub.org) is a flexible Open Source Social Network Kit.

The perfect platform for individual:
* Social Intranets
* Enterprise Social Networks
* Private Social Networks

## DockerHub repository
The images can be found in the [`slobberbone/docker-humhub`](https://hub.docker.com/r/slobberbone/docker-humhub/)
repository.

## Tags
Production:
- [`latest`](humhub/README.md)

Development:
- [`dev`](humhub-dev/README.md)

## Port

This image expose port 443.

## Volume

You can save your humhub directory by mapping them to the volume /var/www/html.

## Usage
```
docker run -d -v /*your_humhub_location*:/var/www/html -p 8035:443 slobberbone/docker-humhub  --link mysql-container:mysql
```
    
### Use Mysql link container

Some o environnement variable are shared with humhumb container, you can use it in the configuraiton screen (example):
MYSQL_PORT_3306_TCP_PORT=3306
MYSQL_PORT_3306_TCP=tcp://172.17.0.2:3306
MYSQL_PORT_3306_TCP_PROTO=tcp
MYSQL_NAME=/mysql-container/mysql
MYSQL_PORT_3306_TCP_ADDR=172.17.0.2
MYSQL_PORT=tcp://172.17.0.2:3306

## Nginx redirection for OMV

Create a configuration file in /etc/nginx/openmediavault-webgui.d/ named humhub.conf wich contains :
```
  location /humhub {
         proxy_pass         http://localhost:8035/humhub;
         proxy_set_header   Host localhost:8035;
          proxy_redirect    default;
  }
```
Then reload nginx configuration :
```
service nginx reload
```
