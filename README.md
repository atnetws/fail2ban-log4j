# fail2ban-log4j
fail2ban filter that catches attacks againts log4j CVE-2021-44228

## Installation
Copy this file to your fail2ban filter.d directory, which is usually something like  
/etc/fail2ban/filter.d  
or similar.  

Add an apache-jndi section to your jail.local or jail.conf:  

```
[apache-jndi]
enabled = true
port = http,https
logpath = /var/log/apache2/access.log
bantime = 86400
maxretry = 1
```

In case you need to monitor multiple sites, wildcards may help:  

```
[apache-jndi]
enabled = true
port = http,https
logpath = /var/www/*/logs/access.log
bantime = 86400
maxretry = 1
```

### Efectiveness  

As of now, this regex catches jndi:ldap requests that contain "jndi:ldap" and one obfuscated version using "lower".  
I'll add more as soon as I find them, but feel free to submit suggestions. 


