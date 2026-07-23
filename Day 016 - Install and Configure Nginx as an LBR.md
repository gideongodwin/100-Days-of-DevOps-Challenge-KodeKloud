## Day 16: Install and Configure Nginx as an LBR

## Task Details:

Day by day traffic is increasing on one of the websites managed by the Nautilus production support team. Therefore, the team has observed a degradation in website performance. 
Following discussions about this issue, the team has decided to deploy this application on a high availability stack i.e on Nautilus infra in Stratos DC.
They started the migration last month and it is almost done, as only the LBR server configuration is pending. Configure LBR server as per the information given below:

- Install `nginx` on the `LBR` (load balancer) server if it is not already installed.
- Configure load-balancing with the `http` context making use of all App Servers. Ensure that you update only the main Nginx configuration file located at `/etc/nginx/nginx.conf`
- Make sure you do not update the apache port that is already defined in the apache configuration on all app servers, also make sure apache service is up and running on all the app servers.
- Once done, you can access the website by running `curl http://stlb01:80` in the terminal.

## Steps:

1. SSH into LBR and verify Nginx
    ```
    ssh loki@stlb01
    sudo -i
    nginx -v
    ```

2. Check App Server Apache port
    ```
    ssh tony@stapp01
    cat /etc/httpd/conf/httpd.conf | grep Listen
    ```

3. Configure load-balancing; edit nginx config
    ```
    vi /etc/nginx/nginx.conf
    ```
    >  Inside the http { ... } block, add a load-balancing upstream section and a server block for the LBR
    
    ```
    upstream app_servers {
        server stapp01:6100;
        server stapp02:6100;
        server stapp03:6100;
    }
    
    server {
        location / {
            proxy_pass http://app_servers;
        }
    }
    ```

4. Test Nginx config
    ```
    nginx -t
    ```

5. Restart Nginx
    ```
    systemctl restart nginx
    ```

6. Test load balancing from LBR server:
    ```
    curl http://stlb01:80
    ```
