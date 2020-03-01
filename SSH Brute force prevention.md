# CentOS SSH auth try limiting
SO that the attacker can be limited. Basically limiting unauthorized. CentOS does not have built in ssh auth protection(I think). Introducing fail2ban. This is the easiest way to secure the ssh

#### Installation

Add a reference to the EPEL project, since the Fail2ban package is not available (yet) in the official CentOS package repo.
```
 sudo yum install epel-release
```
Answer y  when prompted for confirmation.

Install Fail2ban with the following command:
```
sudo yum install fail2ban
```
Enable the Fail2ban service upon system start:
```
sudo systemctl enable fail2ban
```

#### Configuration

Edit a new jail file for ease of use.
```
sudo nano /etc/fail2ban/jail.local
```
```
[DEFAULT]
# Ban hosts for 1 hour after they perform 3 failed login attempts within 10 minutes
bantime = 3600
findtime = 600
maxretry = 3

# Never ban the following space-separated IP addresses/masks
ignoreip = 127.0.0.1/8

# Override /etc/fail2ban/jail.d/00-firewalld.conf 
# to ensure that iptables will be used for firewall configuration
banaction = iptables-multiport

# Choose what to do when issuing a ban:
# $(action_)s : [default] 
#    sets the OS firewall to reject all incoming calls
#    from that IP address for the specified amount of time
# $(action_mw)s : same as above + send and alert e-mail
# $(action_mwl)s : same as above + adds relevant log lines to the e-mail
# action = $(action_)s

# Send fail2ban alerts & warnings to the following e-mail address
destemail = web@ryadel.com
sendername = Fail2Ban
mta = sendmail

[sshd]
# Enables the sshd jail
enabled = true
```

#### Verification

check service
```
sudo systemctl status fail2ban
```

Restart service

```
sudo systemctl restart fail2ban
```
