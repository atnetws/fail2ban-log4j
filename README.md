# fail2ban-log4j
fail2ban filter that catches attacks against log4j CVE-2021-44228

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

Logpath for LAMP servers managed by ispConfig:

```
logpath = /var/www/clients/client*/web*/log/access.log
```

### Effectiveness  

As of now, this regex catches jndi:ldap requests that contain "jndi:ldap" and one obfuscated version using "lower".  
I'll add more as soon as I find them, but feel free to submit suggestions. 

#### Does it work?

Yes and no. From a technical point of view, it does what it is supposed to to. It detects known formats of log4shell attempts and should at least keep those who don't put too much effort in their scans blocked from your machines. Unfortunately, the possibilities of masking / obfuscating these requests are unlimited, so keeping up with all possible RegEx variants might appear like a cat-and-mouse game.

#### Like this?

If this saved you some time, why not [Buy me a coffee](https://www.buymeacoffee.com/atnetws)? ;)

