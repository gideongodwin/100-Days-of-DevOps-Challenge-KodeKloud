## Day 12 - Linux Network Services

## Task Details:

Our monitoring tool has reported an issue in `Stratos` Datacenter. One of our app servers has an issue, as its Apache service is not reachable on `port 3004` (which is the Apache port). The service itself could be down, the firewall could be at fault, or something else could be causing the issue.

- Use tools like `telnet`, `netstat`, etc. to find and fix the issue. Also make sure Apache is reachable from the jump host without compromising any security settings.

- Once fixed, you can test the same using command `curl http://stapp02:3004` command from jump host.

- Note: Please do not try to alter the existing `index.html` code, as it will lead to task failure.

## Steps:

1. Test Connectivity to the App Servers from `jump host`
      ```
      telnet stapp01 3004
      # or
      curl http://stapp01:3004
      ```

2. SSH into the affected server `stapp01` and switch to root user
      ```
      ssh tony@stapp01
      ```
      ```
      sudo -i
      ```

3. Check if Apache service is running
      ```
      systemctl status httpd
      ```

4. Check logs for errors if it fails:
      ```
      journalctl -xeu httpd.service
      ```

5. Find what service is using port 3004
      ```
      lsof -i :3004
      ```

6. Kill the service
      ```
      kill -9 <PID>
      ```

7. Start the Apache service
   ```
   systemctl enable --now httpd
   ```

8. Confirm Apache is listening on 3004
   ```
   ss -tulpn | grep 3004
   ```

9. List firewall rules
    ```
    iptables -L -n
    ```

10. Allow all incoming TCP traffic on port `3004`
      ```
      iptables -I INPUT -p tcp --dport 3004 -j ACCEPT
      ```

11. Save the rule
      ```
      iptables-save > /etc/sysconfig/iptables
      ```
    
12. Restart the Apache service
      ```
      systemctl restart httpd
      ```

13. Go back to the jump host and verify:
      ```
      curl http://stapp01:3004
      ```
