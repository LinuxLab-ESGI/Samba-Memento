# Samba-Memento
<i>Memento to create Samba servers on Linux systems ! </i>
__________

### Prerequisite : 

You can install Samba via these commands :

<i>For Debian distributions :</i>
```
apt install samba -y
```

<i>For RedHat ones :</i>
```
dnf install samba -y
```

Of course, your equipment must be connected on a LAN and preferably with a static address.

>In fact, it will be easier to use and configure the Samba server if the equipment has a static address not provided by a DHCP server.

## I - Create a Samba server

Once the Samba server is installed, create the directory where you want users have to access. With the *mkdir* command create the directory. As an example, we will use <b>/home/pi/shared/public</b>.

Then, edit the configuration file <b>/etc/samba/smb.conf</b> and add the following lines : 

```
[MyAwesomeSambaServer]
path = /home/pi/shared/public
writeable=Yes
create mask=0777
directory mask=0777
public=no

```

Key | Description |
--- | --- |
[MyAwesomeSambaServer]| Name of your Samba configuration, you can freely choose it. Moreover, it defines the point at which you will access the share. For example, ours will be at the following address: <u>\\\raspberrypi\\MyAwesomeSambaServer</u>. |
path| Directory of the folder we created before. |
writeable| When this option is set to “Yes“, it will allow the folder to be writable. |
create mask| This option defines the maximum permissions for files. |
directory mask| This option defines the maximum permissions for folders. |
public| If this is set to “no” the Samba server will require a valid user to grant access to the shared folder. I beg you to set the "no" value ! |

Finally, restart the Samba server to load the new configuration :
```
sudo systemctl restart smbd
```

## II - Authentication to the Samba server

To add a minimum of security, we will create a user with a password to prevent not authorized access to our Samba server. First, enter the command :

```
sudo smbpasswd -a <name_of_the_user>
```

Then, enter the password of the user.

## III - Access to the Samba server

To access to your Samba server, you will need to get the name of your Samba configuration (in this example : MyAwesomeSambaServer) and the NetBios name or the IP address of the server. This access depends of the operating system.


### On Windows :

Follow this tutorial : <i>https://www.techradar.com/how-to/how-to-map-a-network-drive-in-windows-10</i>


### On Mac OS : 

Follow this tutorial : <i>https://www.riohondo.edu/its/how-to-connect-to-a-network-shared-folder-with-mac-os-x/</i>


### On Linux :

Follow this tutorial : https://www.ghacks.net/2009/11/04/connect-to-your-samba-server-from-linux/

__________
<i>Updated : 17/06/2024, Author : Xen0rInspire</i>
