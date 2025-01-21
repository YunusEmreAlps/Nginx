# Nginx Configuration

Before we start with the lesson, let's remember the topics we have covered in the previous lesson. We have learned about the following topics:

- **What is Nginx?**
- **History**
- **Features**
- **Use Cases**
- **Advanced Capabilities**
- **Installation**
- **Basic Configuration Files**
- **Starting and Stopping Nginx**
- **Serving a Static Website**
- **Create an index.html file**

But In this lesson, some of topics and commands keep using the same, so we will not repeat them again. But I added this topic to the lesson to make sure that you remember the previous lesson.

## Installation

Nginx is available in the default repositories of most Linux distributions. You can install Nginx using the following commands:

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

## Nginx Configuration Structure

Nginx configurations are typically found in the **/etc/nginx/nginx.conf** file. The main blocks within this file include `http`, `server`, and `location` blocks, each serving a specific purpose.

- `http`: The http block is the top-level container for web server configuration. Inside this block, you can configure directives like timeouts, file limits, compression, and logging.

- `server`: The server block defines a virtual server. This is where you set up settings for individual domains or IPs.

Example of a basic server block:

```nginx
server {
    listen 80;
    server_name example.com;
    root /var/www/example;
    index index.html;
}
```

- `location`: The location block defines how specific URIs are handled. You can configure multiple location blocks to serve different content for different paths.

```nginx
location / {
    try_files $uri $uri/ =404;
}
```

## Virtual Hosts

Nginx can host multiple websites on a single server using virtual hosts. Virtual hosts allow you to bind different domain names to the same server.

Example Virtual Host Configuration:

```nginx
server {
    listen 80;
    server_name domain1.com;
    root /var/www/domain1;

    location / {
        try_files $uri $uri/ =404;
    }
}

server {
    listen 80;
    server_name domain2.com;
    root /var/www/domain2;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

This setup allows you to host domain1.com and domain2.com on the same server, with separate document roots.

## Important Directives

Understanding these core directives is crucial for configuring Nginx properly.

- `server_name`: Defines the domain name or IP that the server listens to.
- `root`: Sets the directory where Nginx looks for files to serve.
- `index`: Specifies the default file to serve when accessing a directory (e.g., index.html).
- `listen`: Specifies the port on which the server listens (e.g., 80 for HTTP).

## Log Files

Nginx logs both access and error data. By default, log files are stored in **/var/log/nginx/**.

Access Log (Tracks incoming requests):

```bash
/var/log/nginx/access.log
```

Error Log (Stores errors and warnings):

```bash
/var/log/nginx/error.log
```

You can customize logging in your nginx.conf file:

```nginx
http {
    log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log /var/log/nginx/access.log main;
}
```

## Serving a Static Website

- **Create a Directory for Your Site**:

```bash
sudo mkdir -p /var/www/my_website
sudo nano /var/www/my_website/index.html
```

- **Add this content to index.html**:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to Nginx</title>
</head>
<body>
    <h1>Welcome to My Nginx Website!</h1>
</body>
</html>
```

- **Modify Nginx Configuration Edit the Nginx configuration file**:

```bash
sudo nano /etc/nginx/sites-available/default
```

Replace the content with:

```nginx
server {
    listen 80;
    server_name localhost;

    root /var/www/my_website;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

- **Create an index.html file**:

```bash
  sudo nano /var/www/html/index.html
```

The above configuration allows Nginx to serve the **index.html** file in the **/var/www/html** directory. After creating the configuration, restart Nginx to apply the changes and test it by navigating to **<http://localhost>** in your browser.

- **Restart Nginx**:

```bash
  sudo systemctl restart nginx
```

- **Access the website**:

```bash
  curl http://localhost:80.bulutbilisimciler.com
```
