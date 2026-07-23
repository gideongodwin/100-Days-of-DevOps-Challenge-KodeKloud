## Day 20 - Configure Nginx + PHP-FPM Using Unix Sock

## Task Details:

The Nautilus application development team is planning to launch a new PHP-based application, which they want to deploy on Nautilus infra in Stratos DC. 
The development team had a meeting with the production support team and they have shared some requirements regarding the infrastructure. Below are the requirements they shared:

- Install `nginx` on `app server 3` , configure it to use port `8094` and its document root should be `/var/www/html`

- Install `php-fpm` version `8.1` on `app server 3` it must use the unix socket `/var/run/php-fpm/default.sock` (create the parent directories if don't exist).

- Configure `php-fpm` and `nginx` to work together.

- Once configured correctly, you can test the website using `curl http://stapp03:8094/index.php` command from jump host.

  > We have copied two files, `index.php` and `info.php`, under `/var/www/html` as part of the PHP-based application setup. Please do not modify these files

## Steps

1. SSH into app server 3 and switch to root user
   ```
   ssh banner@stapp03
   sudo -i
   ```

2. Install nginx
   ```
   yum install nginx -y
   ```

3. Configure nginx to use port `8094`
    ```
    # Open the main configuration file:
    vi /etc/nginx/nginx.conf
    
    # edit the server block
    server {
        listen 8094;
        listen [::]:8094;
        server_name _;
    
        root /var/www/html;
        index index.html index.php info.php;
    }
    ```

4. Start nginx
    ```
    systemctl start nginx
    ```

5. Install `php-fpm` 8.1
    ```
    # Install the EPEL and Remi repositories.
    sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm -y
    sudo dnf install https://rpms.remirepo.net/enterprise/remi-release-9.rpm -y
    
    # Enable the CodeReady Builder (CRB) repository
    sudo crb enable
    
    # Reset the default PHP module and enable the PHP 8.1 stream
    sudo dnf module reset php -y
    sudo dnf module enable php:remi-8.1 -y
    
    # Install PHP 8.1
    sudo dnf install php php-cli php-fpm -y
    
    # Verify the installation
    php -v
    ```

6. Open the main configuration file:
    ```
    vi /etc/nginx/nginx.conf
    ```

7. Update the server block to configure php-fpm socket
    ```
    server {
        listen 8094;
        listen [::]:8094;
        server_name _;
    
        root /var/www/html;
        index index.html index.php info.php;
    
        include /etc/nginx/default.d/*.conf;
    
        location / {
            try_files $uri $uri/ =404;
        }
    
        error_page 404 /404.html;
        location = /404.html {}
    
        error_page 500 502 503 504 /50x.html;
        location = /50x.html {}
    
        location ~ \.php$ {
            fastcgi_pass unix:/var/run/php-fpm/default.sock;
            fastcgi_index index.php;
            include fastcgi.conf;
        }
    }
    ```

8. Check nginx configuration
   ```
   nginx -t
   ```

9. Test the website
   ```
   curl http://stapp03:8094/index.php
   ```
