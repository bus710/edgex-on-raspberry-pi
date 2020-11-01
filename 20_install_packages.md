[To README](README.md)

# 2. How to install package required for EdgeX development

The Ubuntu server 20.10 is running on the RPI and we can access via SSH. This chapter introduces some items to do before EdgeX installation. 

<br/>

## 2.1 Hostname and Timezone

The RPI has its hostname as "ubuntu", which is fine as long as there are only one machine has the name. However, as a developer runs more RPIs, there are more chances to make mistakes if all the RPIs have same name. To change the name (but pick a editor you like):
```sh
$ sudo vi /etc/hostname
$ sudo reboot # to take effect of the new name
```

Also, the RPI has its timezone as UTC so that scheduled tasks based on local time will not work as expected. To change the timezone:
```sh
# Please pick an area in the list of tzdata
$ sudo dpkg-reconfigure tzdata

# To confirm the new timezone
$ timedatactl
        Local time: Sun 2020-11-01 11:26:43 PST     
    Universal time: Sun 2020-11-01 19:26:43 UTC     
```

<br/>

## 2.3 Update package list

Ubuntu's package management system is based on Debian and Canonical manages Ubuntu's package list. To update the RPI:
```sh
$ sudo apt update
$ sudo apt upgrade
```

<br/>



