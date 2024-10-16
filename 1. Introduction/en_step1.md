# Nginx Introduction and Basic Setup

Nginx is a high-performance web server and reverse proxy server. It is commonly used for serving static content, load balancing, and functioning as a reverse proxy.

## History

Nginx was created by Igor Sysoev in 2002. It was initially developed to solve the C10k problem, which refers to the ability of a server to handle 10,000 concurrent connections. Nginx is known for its high performance, stability, and low resource consumption. It is widely used by high-traffic websites and web applications.

## Features

Nginx offers a wide range of features and capabilities, making it a popular choice for web servers and reverse proxies. Some of the key features of Nginx include:

- **High Performance**: Efficiently handles numerous concurrent connections with minimal resources.
- **Reverse Proxy**: Forwards client requests to other servers/applications.
- **Load Balancing**: Distributes traffic across multiple servers to enhance performance and reliability.
- **Caching**: Stores static content to reduce load and improve speed.
- **SSL/TLS Termination**: Manages secure connections, handling encryption and decryption.
- **WebSockets Support**: Enables real-time client-server communication.
- **HTTP/2 Support**: Improves performance and efficiency over HTTP/1.1.
- **Modular Architecture**: Easily extendable with various modules for security, monitoring, and more.
- **Flexible Configuration**: Customizable with a simple, intuitive configuration language.
- **Open Source**: Released under the 2-clause BSD license, with active community support.
- **Scalability & Security**: Built to scale and secure web applications against vulnerabilities.

## Use Cases

Nginx is commonly used in a variety of scenarios, including:

- **Web Server**: Serving static and dynamic content for websites and web apps.
- **Reverse Proxy**: Forwarding requests to backend services or other servers.
- **Load Balancer**: Distributing traffic across multiple backend servers.
- **Caching**: Storing and serving cached content to improve performance.
- **SSL/TLS Termination**: Managing encrypted connections between clients and servers.
- **WebSockets**: Supporting real-time data exchanges in applications.
- **Microservices Gateway**: Routing requests to different microservices.
- **Content Delivery**: Acting as a CDN to accelerate content delivery via caching.
- **High Availability**: Ensuring uptime with reliable, fault-tolerant setups.
- **Security Enhancements**: Protecting against common web vulnerabilities.
- **Monitoring & Logging**: Capturing detailed logs for traffic, errors, and performance metrics.
- **DevOps Integration**: Automating deployment and server management tasks in cloud and container environments.

## Advanced Capabilitiess

- **HTTP/2**: Optimized communication for faster web performance.
- **WebSocket Support**: Real-time, bidirectional communication.
- **SSL/TLS**: Secure connections with advanced encryption features.
- **Customizable Modules**: Extend functionality with security, logging, and caching modules.
- **Integration**: Seamless compatibility with other services like Docker, Kubernetes, and CI/CD pipelines.

In this lab, we will cover the basic installation and configuration of Nginx on a Linux server.

## Installation

- **Ubuntu/Debian**:

```bash
  sudo apt-get install nginx
```

- **CentOS/RHEL**:

```bash
  sudo yum install nginx
```

- **macOS**: (We are not using macOS in this scenario, but if you want to install your local machine, you can use the following command)

```bash
  brew install nginx
```

- **Docker**:

```bash
  docker pull nginx

  # Run Nginx container
  docker run -d -p 80:80 nginx

  # Access Nginx container
  docker exec -it <container_id> /bin/bash

  # Stop Nginx container
  docker stop <container_id>

  # Remove Nginx container
  docker rm <container_id>

  # Remove Nginx image
  docker rmi nginx

  # Check Nginx logs
  docker logs <container_id>

  # Check Nginx container status
  docker ps -a | grep nginx
```

## Basic Configuration Files

The main configuration settings are typically found in **/etc/nginx/nginx.conf**. For site-specific configurations, the directories **/etc/nginx/sites-available/** and **/etc/nginx/sites-enabled/** are used.

## Starting and Stopping Nginx

- **Start Nginx**:

```bash
  sudo systemctl start nginx
```

- **Stop Nginx**:

```bash
  sudo systemctl stop nginx
```

- **Restart Nginx**:

```bash
  sudo systemctl restart nginx
```

- **Check Nginx Status**:

```bash
  sudo systemctl status nginx
```

## Serving a Static Website

To serve a static website with Nginx, create a configuration file in the **/etc/nginx/** directory. Here's an example **nginx.conf** file:

```bash
  # Change the directory to the Nginx configuration directory
  cd /etc/nginx

  # list the files in the directory
  ls

  # Change default configuration file
  mv nginx.conf old.nginx.conf
  
  # you can use nano or vim to create the file
  apt-get install nano
  nano /etc/nginx/nginx.conf

  # you can use vim
  apt-get install vim
  vim /etc/nginx/nginx.conf
```

- **nginx.conf**:

```nginx
events {}

http {
  server {
    listen 80;
    server_name localhost;

    root /var/www/html;
    index index.html;
  }
}
```

- **Test the configuration file**:

```bash
  sudo nginx -t
```

- **Create an index.html file**:

```bash
  sudo nano /var/www/html/index.html
```

- **index.html**:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Welcome to Nginx</title>
</head>
<body>
  <h1>Welcome to Bulut Bilişimciler!</h1>
  <p>This is a sample website served by Nginx.</p>
</body>
</html>
```

After creating the configuration file, restart Nginx to apply the changes.

- **Restart Nginx**:

```bash
  sudo systemctl restart nginx
```

- **Access the website**:

```bash
  curl http://localhost:80.bulutbilisimciler.com
```
