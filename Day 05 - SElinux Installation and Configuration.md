## Day 5: SElinux Installation and Configuration

#### Task Details:
Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for `App server 1` in the Stratos Datacenter:
- Install the required `SELinux` packages.
- Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.
- No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.
- Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled.

#### STEPS:
1. Connect to the first app server and switch to root user
   ```
   ssh banner@stapp03`
   sudo -i
   ```
   > When prompted, enter the password for user `banner`

2. Install SELinux packages
   ```
   yum install selinux* --skip-broken -y`
   ```

3. Edit the SELinux config file:
   ```
   vi /etc/selinux/config
   ```
   Find this line:
   ```
   SELINUX=enforcing
   ```
   Change it to:
   ```
   SELINUX=disabled
   ```

4. Verify the current status:
   ```
   sestatus
   ```
