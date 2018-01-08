# Web server administration on Ubuntu 16.04 LTS

## Commands

## Firewall - ufw

## NGINX as web server

### Installing NGINX
```bash
sudo apt-get install nginx
```
### NGINX web server configuration
nginx configuration file (`nginx.conf`) is located in `/etc/nginx/' directory. All directives in the configuration wi;; end with a semi-colon `;` 
#### Configuration format
```bash
http{
    server{
        location / {
            root /var/www/nginx/html;
            index index.html index.htm;
        }
    }
}
```
Configuration is modular underneath the `http` parent and we can create `server` entries. `Location` entries can be found within server blocks. A single server entry is sufficient but more than one server entry is equivalent to creating *VirtualHosts* in Apache.
#### Restrict Access
```bash
location / {
    root /var/www/nginx/html;
    index index.html index.htm;

    allow 127.0.0.1;
    allow 192.168.56.0/24;

    deny all;
}
```
Access to `locations` can be managed using `allow` or `deny` directive.
### Using NGINX as a reverse Proxy Server
#### Reverse proxy
A reverse proxy listens at a specific TCP port on the web server and redirect the incoming requests to specific directories or TCP ports. This is really useful when you have one static IP and want to host multiple web sites that using different technologies.

_E.g:_
1. www.site1.com is asp.net web app hosted (Uses Supervisor) at port 5000
2. www.site2.com is asp.net web app hosted (Uses Supervisor) at port 5001
3. www.site3.com is asp.net web app hosted (Uses Supervisor) at port 5003
4. www.blog1.com is wordpress site hosted (Uses LAMP) at port 8001
5. www.blog2.com is wordpress site hosted (Uses LAMP) at port 8002
6. www.blog3.com is wordpress site hosted (Uses LAMP) at port 8003

in the above configuration, nginx will listen to `TCP Port 80` on the web server and redirect all requests to its respective `TCP Port`.
```bash
http {
    server {
        location /balancer/{
            proxy_pass http://192.168.56.10/
        }
    }
}
```
The `proxy_pass` directive in a `location` block can redirect the URL to reverse proxy location. *Note*: The end of *location_ url and *proxy_pass* url must be a *forward slash "/"* when referring to directories rather than pages.

## MYSQL

## SQL Server

## Node.js hosting

## Wordpress hosting

## ASP.Net Core hosting
### .Net Core
### Supervisor

## Postfix