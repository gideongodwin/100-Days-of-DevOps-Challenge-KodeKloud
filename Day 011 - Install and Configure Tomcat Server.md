## Day 11 - Install and Configure Tomcat Server

## Task Details:

The Nautilus application development team recently finished the beta version of one of their Java-based applications, which they are planning to deploy on one of the app servers in Stratos DC. 

After an internal team meeting, they have decided to use the tomcat application server. Based on the requirements mentioned below complete the task:

- Install `tomcat server` on `App Server 2`

- Configure it to run on port `6300`

- There is a `ROOT.war` file on `Jump host` at location `/tmp`

- Deploy it on this tomcat server and make sure the webpage works directly on base URL i.e `curl http://stapp02:6300`

## Steps:

1. SSH into App Server 2
   ```
   ssh steve@stapp02
   ```

2. Install Tomcat
   ```
   sudo yum install -y tomcat
   ```

3. Find the Connector port line: Change `8080` to `6300` in the configuration file
   ```
   sudo vi /etc/tomcat/server.xml
   ```

4. From the Jump Host, copy the file to App Server 2
   ```
   scp /tmp/ROOT.war steve@stapp02:/tmp/
   ```

5. Then SSH to App Server 2
   ```
   ssh steve@stapp02
   ```

6. On App Server 2, move it to the webapps folder:
   ```
   sudo mv /tmp/ROOT.war /usr/share/tomcat/webapps/
   ```

7. Start and Enable Tomcat
   ```
   sudo systemctl enable --now tomcat
   ```

8. Verify Deployment
   ```
   curl http://stapp02:6300
   ```
