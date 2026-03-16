## Day 11: Install and Configure Tomcat Server

#### TASK DETAILS:
The Nautilus application development team recently finished the beta version of one of their Java-based applications, which they are planning to deploy on one of the app servers in Stratos DC. After an internal team meeting, they have decided to use the tomcat application server. Based on the requirements mentioned below complete the task:
a. Install `tomcat server` on `App Server 2`
b. Configure it to run on port `6300`
c. There is a `ROOT.war` file on `Jump host` at location `/tmp`

Deploy it on this tomcat server and make sure the webpage works directly on base URL i.e `curl http://stapp02:6300`

#### STEPS:
1. SSH into App Server 2 \
   `ssh steve@stapp02`

2. Install Tomcat \
   `sudo yum install -y tomcat`

3. Find the Connector port line: Change `8080` to `6300` \
   `sudo vi /etc/tomcat/server.xml`

4. Login to the Jump Host and copy the file to App Server 2 \
   `scp /tmp/ROOT.war steve@stapp02:/tmp/`

5. Then SSH to App Server 2 \
   `ssh steve@stapp02`

6. Move the WAR file to Tomcat deployment directory \
   `sudo mv /tmp/ROOT.war /usr/share/tomcat/webapps/`

7. Start and Enable Tomcat \
   ```
   sudo systemctl start tomcat
   sudo systemctl enable tomcat

8. Verify Deployment \
   `curl http://stapp02:6300`
