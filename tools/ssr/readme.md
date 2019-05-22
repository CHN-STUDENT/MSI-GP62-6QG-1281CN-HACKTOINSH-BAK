# How to install SSR in Mac OS


## Install the brew

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)
```

## Install the python3

```
brew install python3
```

## Install the libsodium

```
brew install libsodium
```

## Install the screen

```
brew install screen
```

## Clone the SSR-Backup Project From Github

```
git clone https://github.com/shadowsocksrr/shadowsocksr.git
```

## Create your SSR Config File
    vim /etc/ssr.json
Your config looks like this:
```
{
    "server" : "yoursever",
    "server_port" : xxx,
    "server_udp_port" : 0,
    "password" : "xxxxxx",
    "method" : "chacha20",
    "protocol" : "auth_chain_a",
    "protocolparam" : "",
    "obfs" : "tls1.2_ticket_auth",
    "obfsparam" : "xxxxxx",
    "udp_over_tcp" : false,
    "local_address": "127.0.0.1",
    "local_port": 1080
}
```
## Create a start script
    sudo vim ssr.sh
It looks like this:
```bash
#!/bin/bash

screen /usr/local/bin/python3 ./shadowsocksr/shadowsocks/local.py -c /etc/ssr.json >> ssr.log
```
## Download Chromium Extension Named SwitchyOmega on Its GitHub Project Release
> URL: https://github.com/FelisCatus/SwitchyOmega/releases

Then try to install it on your Chromium. Set the proxy config.

    sockv5 127.0.0.1 1080
    
## Also,We Can Use Proxychians To Set CLi Command Proxy

```
brew install proxychains-ng
```

## Set proxychians config file
```
vim /usr/local/etc/proxychains.conf
```

It looks like this:
```
 # proxychains.conf  VER 3.1
#
#        HTTP, SOCKS4, SOCKS5 tunneling proxifier with DNS.
#	

# The option below identifies how the ProxyList is treated.
# only one option should be uncommented at time,
# otherwise the last appearing option will be accepted
#
#dynamic_chain
#
# Dynamic - Each connection will be done via chained proxies
# all proxies chained in the order as they appear in the list
# at least one proxy must be online to play in chain
# (dead proxies are skipped)
# otherwise EINTR is returned to the app
#
strict_chain
#
# Strict - Each connection will be done via chained proxies
# all proxies chained in the order as they appear in the list
# all proxies must be online to play in chain
# otherwise EINTR is returned to the app
#
#random_chain
#
# Random - Each connection will be done via random proxy
# (or proxy chain, see  chain_len) from the list.
# this option is good to test your IDS :)

# Make sense only if random_chain
#chain_len = 2

# Quiet mode (no output from library)
#quiet_mode

# Proxy DNS requests - no leak for DNS data
proxy_dns 

# Some timeouts in milliseconds
tcp_read_time_out 15000
tcp_connect_time_out 8000

# ProxyList format
#       type  host  port [user pass]
#       (values separated by 'tab' or 'blank')
#
#
#        Examples:
#
#            	socks5	192.168.67.78	1080	lamer	secret
#		http	192.168.89.3	8080	justu	hidden
#	 	socks4	192.168.1.49	1080
#	        http	192.168.39.93	8080	
#		
#
#       proxy types: http, socks4, socks5
#        ( auth types supported: "basic"-http  "user/pass"-socks )
#
[ProxyList]
# add proxy here ...
# meanwile
# defaults set to "tor"
socks5 	127.0.0.1 1080
```

## How to use
    chmod a+x ssr.sh
    ./ssr.sh
    proxychains4 brew install openssl
