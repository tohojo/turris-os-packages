# DNS over TLS

UCI configuration for DNS-over-TLS is located in **/etc/config/resolver**. You can enable redirection to custom DNS resolver by setting option **forward_custom**.

 **Example:**
```
uci set resolver.common.forward_custom='cloudflare-dns'
uci commit resolver
```
Where  cloudflare-dns is name defined in config file from /etc/resolver/dns_servers or name defined in dns_server config section in /etc/config/resolver

Configuration files for DNS server are located in /etc/resolver/dns_servers directory and they have **config** suffix.

**Example of content of configuration file:**
```
name="cloudflare-dns"
description="something something darkside..."
enable_tls="1"
port="853"
ipv4="1.1.1.1"
ipv6="2606:4700:4700::1111"
pin_sha256="yioEpqeR4WtDwE9YxNVnCEkTxIjx6EEIwFSQW+lJsbc="
```

> Note: Config files shouldn't be modified by users because they'll be rewrited after every update.

If you want to edit configuration for a particular server you should create **dns_server** section **/etc/config/resolver** with same name as is defined in config file and change value of desired variable. System will prefere option set inside UCI config.

**Example of new section inside /etc/config/resolver**
```
config dns_server
	option name 'cloudflare-dns'
	option port "888"
```
This will change port to 888 other options will be read from /etc/resolver/dns_server/*.config file.
