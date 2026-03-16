## Day 13: IPtables Installation And Configuration

#### TASK DETAILS:

We have one of our websites up and running on our `Nautilus` infrastructure in `Stratos DC`
Our security team has raised a concern that right now Apache’s port i.e `3000` is open for all since there is no firewall installed on these hosts.
So we have decided to add some security layer for these hosts and after discussions and recommendations we have come up with the following requirements:

1. Install `iptables` and all its dependencies on each app host.
2. Block incoming port `3000` on all apps for everyone except for LBR host.
3. Make sure the rules remain, even after system reboot.

#### STEPS:
1. SSH into App Server 1 \
   `ssh tony@stapp01`

2. Install iptables and enable the service \
```
yum install -y iptables iptables-services
systemctl enable iptables
systemctl start iptables
```
3. Allow LBR host to access port `3000` and block everyone else on port `3000`
```
iptables -I INPUT 1 -p tcp -s 10.244.195.218 --dport 3000 -j ACCEPT && iptables -I INPUT 2 -p tcp --dport 3000 -j DROP
```

4. Save rules
```
iptables-save > /etc/sysconfig/iptables
```

5. You can verify rules with:
```
iptables -L -n
```

6. Run all the above commands on the remaining servers `stapp02` and  `stapp03`

