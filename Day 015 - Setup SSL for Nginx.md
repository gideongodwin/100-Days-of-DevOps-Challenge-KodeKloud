## Day 15: Setup SSL for Nginx

## Task Details:
The system admins team of xFusionCorp Industries needs to deploy a new application on App Server 3 in Stratos Datacenter \
They have some pre-requites to get ready that server for application deployment. Prepare the server as per requirements shared below:

1. Install and configure `nginx` on `App Server 3`

2. On `App Server 3` there is a self signed SSL certificate and key present at location `/tmp/nautilus.crt` and `/tmp/nautilus.key` Move them to some appropriate location and deploy the same in Nginx.

3. Create an `index.html` file with content `Welcome!` under Nginx document root.

4. For final testing try to access the `App Server 3` link (via hostname) from `jump host` using curl command. For example: `curl -Ik https://<app-server-name>/`

## Steps:

1. SSH into App Server 3 and switch to root user
    ```
    ssh banner@stapp03
    sudo -i
    ```

2. Install Nginx
    ```
    yum install -y nginx
    ```

3. Create a dedicated directory to store SSL files
    ```
    mkdir -p /etc/nginx/ssl
    ```

4. Move the existing certificate and key from /tmp into this directory
    ```
    mv /tmp/nautilus.crt /etc/nginx/ssl/nautilus.crt
    mv /tmp/nautilus.key /etc/nginx/ssl/nautilus.key
    ```
5. Configure Nginx for SSL
    ```
    vi /etc/nginx/nginx.conf
    ```

6. Update the Server Block
    ```
    ssl_certificate: "/etc/nginx/ssl/nautilus.crt";
    ssl_certificate_key:"/etc/nginx/ssl/nautilus.key";
    ```

7. Create Test Web Page
    ```
    echo "Welcome!" > /usr/share/nginx/html/index.html
    ```
8. Test Nginx Configuration
    ```
    nginx -t
    ```
9. Start and enable Nginx
    ```
    systemctl start nginx
    systemctl enable nginx
    ```
10. Exit the server
    ```
    exit
    exit
    ```
11. Final Testing from Jump Host
    ```
    curl -Ik https://stapp03
    ```
