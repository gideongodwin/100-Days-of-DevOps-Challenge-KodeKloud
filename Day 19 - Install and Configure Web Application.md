## Day 19 - Install and Configure Web Application

## Task Details:

xFusionCorp Industries is planning to host two static websites on their infra in Stratos Datacenter. 
The development of these websites is still in-progress, but we want to get the servers ready. Please perform the following steps to accomplish the task:

- Install `httpd` package and dependencies on `app server 2`

- Apache should serve on port `8086`

- There are two website's backups `/home/thor/blog` and `/home/thor/cluster` on `jump_host`

  > Set them up on Apache in a way that blog should work on the link `http://localhost:8086/blog/` and cluster should work on link `http://localhost:8086/cluster/` on the mentioned app server.

- Once configured you should be able to access the website using curl command on the respective app server, i.e `curl http://localhost:8086/blog/` and `curl http://localhost:8086/cluster/`

## Steps:

1. SSH into app server 2
   ```
   ssh steve@stapp02
   ```

2. Install Apache
    ```
    sudo yum install -y httpd
    ```

3. Configure Apache to use port `8086`
    ```
    vi /etc/httpd/conf/httpd.conf
    ## Change Listen 80 to Listen 8086
    Listen 8086
    ```

4.  From the jump host, copy the blog and cluster directories to app server 2:
    ```
    scp -r blog steve@stapp02:/home/steve/
    scp -r cluster steve@stapp02:/home/steve/
    ```
    > Enter the password for steve when prompted

5. On app server 2, move the copied directories to `/var/www/html`
    ```
    sudo mv * /var/www/html/
    ```

6. Start and enable Apache
    ```
    sudo systemctl restart httpd
    sudo systemctl enable httpd
    ```

7. Test the websites
    ```
    curl http://stapp02:8086/blog/
    curl http://stapp02:8086/cluster/
    ```
