## Day 6: Create a Cron Job

#### Task Details:
The `Nautilus` system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in `Stratos DC` on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:
a. Install `cronie` package on all `Nautilus` app servers and start `crond` service.
b. Add a cron `*/5 * * * * echo hello > /tmp/cron_text` for root user.

#### STEPS:
1. Connect to the first app server \
   `ssh tony@stapp01`
- When prompted, enter the password for user `tony`

2. Switch to Root User \
   `sudo -i`   
3. Install cronie, start and verify crond service:
  ```
  yum install cronie -y
  systemctl start crond
  systemctl status crond
  ```
4. Add the cron job:
```
crontab -e
```
   Insert the following line:
```
*/5 * * * * echo hello > /tmp/cron_text
```

5. Verify the cron job: \
   `crontab -l`

6. Run all the above commands on the remaining servers


