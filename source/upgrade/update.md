# Gluu Server Update Package

Gluu Server update packages are released to fix urgent issues, with low 
impact on deployment. Normally these involve updates to the java code,
effected replacing the `war` file. These are installed using 
`yum` or `apt-get` command.

##Check version of installed Gluu CE server.
- Version of the server can be found from the name of the installed home Gluu directory
- Below is an alternate method to determine the version of the installed CE server.
 
 `oxTrust version: cat /opt/tomcat/webapps/identity/META-INF/MANIFEST.MF`
 `oxAuth version: cat /opt/tomcat/webapps/oxauth/META-INF/MANIFEST.MF`
 
 ![image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/gluu-verify-version.png)
 
 
## Backup

It is highly recommended to stop the Gluu Server, and `tar` 
folder `/opt/gluu-server-2.4.4` to ensure speedy recovery from any 
unexpected hiccup. If the organization has any other contingency plans,
that is ok too.

!!! Warning
    Please make sure that there is enough disk space to tar the entire 
    Gluu Server, at least 4GB of Disk Space is recommended.

Use the following commands to tar the Gluu Server folder from the host
OS:

```
# service gluu-server-2.4.4 stop
# tar cvf gluu244-backup.tar /opt/gluu-server-2.4.4/
```

## Install Update Package

Gluu Server update packages are available from the Gluu Repository.
Make sure to stop Gluu Server before installing and finalizing the 
update package.

* **CentOS 6.x/7.2, RHEL 6/7:** 

```
# yum update
# service gluu-server-2.4.4 stop
# yum install gluu-updater-2.4.4

```

* **Ubuntu Server 14.04/16.04, Debian 8:** 

```
# apt-get update
# service gluu-server-2.4.4 stop
# apt-get install gluu-updater-2.4.4

```

After the update package is installed, use the following commands to 
finalize the installation by running the update script. 

```
# service gluu-server-2.4.4 start
# service gluu-server-2.4.4 login
# cd /opt/upd/2.4.4.sp2/bin
# ./update_war.sh
```

Upon successful update, check the version again to confirm on the update.

** NOTE: It is recommended to wait for few minutes while the changes take place and 
Gluu Server CE can be used.**