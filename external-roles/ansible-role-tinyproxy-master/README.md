Ansible Role: Tinyproxy
=========

**Internet-proxy role. Used to setup tinyproxy server.** 

Role installs tinyproxy server and sets it up by copying config and filter files.
Current configuration block connections to any sources exclude ones that are listed in filter file.
Variables for tinyproxy server are in  repository -  **_group-vars/internet-proxy-prod.yml_** There are only variables related to whitelist-filter file. Config file is in **_files/tinyproxy.conf_** and template for filter-file is in **_templates/tinyproxy_filter.j2_**

For using proxy on target host you may add the following lines to your **_/etc/environment_** file:
```
http_proxy="http://internet-proxy.dc:3128/"
https_proxy="https://internet-proxy.dc:3128/" 
```
and than run the following commands on the bash shell:
```
export http_proxy="http://internet-proxy.dc:3128/"
export https_proxy="https://internet-proxy.dc:3128/"
```
or even better way is to configure only specific services to use proxy, for example pagerduty, by editing /etc/init.d/pdagent as the root user.
```
PID_FILE=$PID_DIR/pdagentd.pid

export http_proxy=http://internet-proxy.dc:3128/
export https_proxy=https://internet-proxy.dc:3128/
```
Note: Be sure to restart the PagerDuty Agent with the command service pdagent restart.


