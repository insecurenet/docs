Authenticating OpenVPN Users with RADIUS via Active Directory
=============================================================

This how-to article will show how to set up OpenVPN on pfSense®
software for Windows clients, using certificates with user
authentication via RADIUS in Active Directory.

This how-to is intended for small businesses that want to roll out
secure VPN connectivity for their users using free software. Due to the
nature of its set up, which is mostly manual, this process may be too
inefficient for larger businesses.

Versions
^^^^^^^^

-  pfSense software version 2.x
-  Active Directory on Windows Server 2008 R2 - I'm using a Forest
   Functional Level of 2008 R2 but I don't think that's really a
   prerequisite. If it doesn't work, user account passwords may need to
   be stored using reversible encryption but since that is a serious
   security issue, it is better to upgrade to at least 2008 R2.

On security and a disclaimer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

I am not a security expert. However the method described in this article
is they way it should be:

-  Two-factor authentication: something you have (the installed
   certificate) and something you know (AD user account name and
   password);
-  The connection is encrypted and nothing crosses the Internet in plain
   text.

If a laptop gets stolen, no one can dial into the corporate network if
they don't know a username and password. If someone guesses a password,
they will also need the certificate to dial in.

I can not guarantee that no bad things happen because of following this
how-to. Please consult other sources, use common sense and try breaking
into the system to check if it's safe.

Thanks
^^^^^^

Thanks to the pfSense forum, in particular to user unguzov, who wrote a
shorter version of this how-to. I adapted his version and added
screenshots. Thanks to Evan Jensen for providing some English version
screenshots. Thanks to Dan, who alerted me on the question of the policy
order.

On the Active Directory domain controller
-----------------------------------------

Create a group VPNusers
^^^^^^^^^^^^^^^^^^^^^^^

Create a security group in Active Directory Users and Computers called
*VPNusers*. Everyone could have access but it's a good idea to keep some
granular control over it.

.. image:: /_static/vpn/openvpn/radiusvpn_204.jpg
   :align: center

Add all accounts that need to use the VPN system to this group.

.. image:: /_static/vpn/openvpn/radiusvpn_205.jpg
   :align: center

Install and configure RADIUS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If RADIUS isn't already set up, add the role to the Domain Controller.
If it is set up, skip this step.

Open **Server Manager** and click the **Roles** node in the tree on the
left.

.. image:: /_static/vpn/openvpn/radiusvpn_003.jpg
   :align: center

On the right side, click **Add Roles**.

.. image:: /_static/vpn/openvpn/radiusvpn_003.jpg
   :align: center

This will open the Add Roles Wizard.

.. image:: /_static/vpn/openvpn/radiusvpn_005.jpg
   :align: center

Check **Network Policy and Access Services**.

.. image:: /_static/vpn/openvpn/radiusvpn_006.jpg
   :align: center

Select **Network Policy Server**.

.. image:: /_static/vpn/openvpn/radiusvpn_010.jpg
   :align: center

If all went well there is now a ***Network Policy and Access Services***
node in the tree.

.. image:: /_static/vpn/openvpn/radiusvpn_011.jpg
   :align: center

Expand the **Network Policy and Access Services** node, go to **NPS
(Local)** > **RADIUS Clients and Servers**, right-click **RADIUS
Clients** and choose **New**.

.. image:: /_static/vpn/openvpn/radiusvpn_012.jpg
   :align: center

In the **Friendly name** field, enter **pfSense VPN** or anything deemed
appropriate. In the **Address (IP or DNS)** field, enter the IP address
of the pfSense firewall. Mine is *192.168.77.1*. **Shared Secret**:
check **Generate** and save the shared secret; It will be needed later
on.

.. image:: /_static/vpn/openvpn/radiusvpn_123.jpg
   :align: center

Under **NPS (Local)** > **Policies** right-click **Network Policies**
and select **New**.

.. image:: /_static/vpn/openvpn/radiusvpn_014.jpg
   :align: center

In the **Policy name** field, enter **Allow pfSense**. **Type of network
access server**: **Unspecified**.

.. image:: /_static/vpn/openvpn/radiusvpn_015.jpg
   :align: center

In the **Specify Conditions** window, click **Add...**

.. image:: /_static/vpn/openvpn/radiusvpn_016.jpg
   :align: center

Select **Windows Groups** and click **Add...**

.. image:: /_static/vpn/openvpn/radiusvpn_017.jpg
   :align: center

Click **Add Groups...** and add the group **VPNusers** (or whatever
group is needed).

.. image:: /_static/vpn/openvpn/radiusvpn_124.jpg
   :align: center

Back in the **Specify Conditions** window, click **Next** and select
**Access granted**.

.. image:: /_static/vpn/openvpn/radiusvpn_020.jpg
   :align: center

Put the new policy before policies preventing the connection. Mind the
**Processing Order** field. Thanks to Dan for alerting me on this.

.. image:: /_static/vpn/openvpn/radiusvpn_999.jpg
   :align: center

In the **Configure Authentication Methods** window, check **Unencrypted
authentication (PAP, SPAP)**.

.. image:: /_static/vpn/openvpn/radiusvpn_021.jpg
   :align: center

Skip the next wizard window (**Constraints**) or configure it if
desired. I suggest leaving it as it is until after confirming the VPN
works.

It's done. Next, Next, Finish until the end.

On the pfSense firewall
-----------------------

Set up the Authentication Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the pfSense webGUI, go to **System > User Manager**, on the 
**Servers** tab. Click |fa-plus| on the right.

.. image:: /_static/vpn/openvpn/radiusvpn_022.jpg
   :align: center

Enter these values:

+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Descriptive name            | RADIUS                                                                                                                                                                                     |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Type                        | Radius                                                                                                                                                                                     |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Hostname or IP address      | 192.168.77.15                                                                                                                                                                              |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Shared Secret               | Paste the shared secret generated by the RADIUS server. Then delete the file containing the shared secret. It will not be needed again and if it is, a new one may be generated instead.   |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Services offered            | Authentication and Accounting                                                                                                                                                              |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Authentication port value   | 1812                                                                                                                                                                                       |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Accounting port value       | 1813                                                                                                                                                                                       |
+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. image:: /_static/vpn/openvpn/radiusvpn_023.jpg
   :align: center

Install a Certificate Authority
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Go to **System > Cert Manager**, **CAs** tab and click |fa-plus|.

.. image:: /_static/vpn/openvpn/radiusvpn_024.jpg
   :align: center

Enter these values:

+----------------------+--------------------------------------------+
| Descriptive name     | TestDomain VPN CA                          |
+----------------------+--------------------------------------------+
| Method               | Create an internal Certificate Authority   |
+----------------------+--------------------------------------------+
| Key length           | 2048                                       |
+----------------------+--------------------------------------------+
| Lifetime             | | 3650 days                                |
|                      | | Ten years should be enough for now.      |
+----------------------+--------------------------------------------+
| Distinguished name   | *Fill out the preferences here.*           |
+----------------------+--------------------------------------------+
| Common name          | testdomainvpn-ca                           |
+----------------------+--------------------------------------------+

.. image:: /_static/vpn/openvpn/radiusvpn_025.jpg
   :align: center

Note that now there is an extra CA in the CA list.

.. image:: /_static/vpn/openvpn/radiusvpn_026.jpg
   :align: center

Create an internal certificate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Go to **System > Cert Manager**, **Certificates** tab and click |fa-plus|.

.. image:: /_static/vpn/openvpn/radiusvpn_027.jpg
   :align: center

Enter these values:

+-------------------------+------------------------------------+
| Method                  | Create an internal Certificate     |
+-------------------------+------------------------------------+
| Descriptive name        | vpn-testdomain-network             |
+-------------------------+------------------------------------+
| Certificate Authority   | TestDomain VPN CA                  |
+-------------------------+------------------------------------+
| Key length              | 2048                               |
+-------------------------+------------------------------------+
| Certificate Type        | Server Certificate                 |
+-------------------------+------------------------------------+
| Lifetime                | 3560 days                          |
+-------------------------+------------------------------------+
| Distinguished name      | *Fill out the preferences here.*   |
+-------------------------+------------------------------------+
| Common Name             | vpn.example.com                    |
+-------------------------+------------------------------------+

Set up the OpenVPN server
^^^^^^^^^^^^^^^^^^^^^^^^^

Go to **VPN > OpenVPN**, **Servers** tab and click |fa-plus|.

.. image:: /_static/vpn/openvpn/radiusvpn_031.jpg
   :align: center

Enter these values:

+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Server Mode:                 | Remote Access ( SSL/TLS User Auth)                                                                                                                                                                                                                                                                                                                                                        |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Backend for authentication   | RADIUS                                                                                                                                                                                                                                                                                                                                                                                    |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Protocol                     | UDP                                                                                                                                                                                                                                                                                                                                                                                       |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Device Mode                  | tun                                                                                                                                                                                                                                                                                                                                                                                       |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Interface                    | WAN                                                                                                                                                                                                                                                                                                                                                                                       |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Local port                   | 1194                                                                                                                                                                                                                                                                                                                                                                                      |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Description                  | Something appropriate                                                                                                                                                                                                                                                                                                                                                                     |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| TLS Authentication           | Check both **Enable authentication of TLS packets** and **Automatically generate a shared TLS authentication key**.                                                                                                                                                                                                                                                                       |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Peer Certificate Authority   | TestDomain VPN CA                                                                                                                                                                                                                                                                                                                                                                         |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Server Certificate           | vpn-testdomain-network (CA: TestDomain VPN CA)                                                                                                                                                                                                                                                                                                                                            |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| DH Parameters Length         | 1024                                                                                                                                                                                                                                                                                                                                                                                      |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Encryption algorithm         | | AES-128-CBC (128-bit)                                                                                                                                                                                                                                                                                                                                                                   |
|                              | | Others probably work as well.                                                                                                                                                                                                                                                                                                                                                           |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Hardware Crypto              | No Hardware Crypto Acceleration                                                                                                                                                                                                                                                                                                                                                           |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Certificate Depth            | One (Client Server)                                                                                                                                                                                                                                                                                                                                                                       |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Strict User/CN Matching      | If this is checked, a user can only connect with their own credentials, not that of other users. I think this is is good idea, so check this option.                                                                                                                                                                                                                                      |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Tunnel Network               | | 192.168.82.0/24                                                                                                                                                                                                                                                                                                                                                                         |
|                              | | Or any other network, as long as it is not in use in the LAN/WAN and probably not at users' locations. i.e. don't use *192.168.0.0/24*, *192.168.1.0/24* and *10.0.0.0/24*.                                                                                                                                                                                                             |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Redirect Gateway             | If this is checked, not only traffic to the LAN will be routed through the tunnel but also to the rest of the Internet. If the user starts downloading a movie it will go through the company network. On the other hand, they will be behind the corporate firewall. Check this to use the VPN for secure Internet access. Do not check if the corporate line has a slow upload speed.   |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Local Network                | | 192.168.77.0/24                                                                                                                                                                                                                                                                                                                                                                         |
|                              | | This is my range. Enter the actual LAN subnet here.                                                                                                                                                                                                                                                                                                                                     |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Concurrent connections       | Crypto can be tough on resources. If the pfSense installation runs on an appliance keep this number low. If it runs on an old computer it can do more. Keep en eye on the machine's CPU. If more concurrent VPN connections ask too much of resources, `upgrade the hardware <https://store.netgate.com>`_.                                                                               |
|                              |                                                                                                                                                                                                                                                                                                                                                                                           |
|                              | I tend to set this number to the number of client installations.                                                                                                                                                                                                                                                                                                                          |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Compression                  | Check, unless clients and server are on stone-age hardware.                                                                                                                                                                                                                                                                                                                               |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Type-of-Service              | Unchecked                                                                                                                                                                                                                                                                                                                                                                                 |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Inter-client communication   | Unchecked unless needed.                                                                                                                                                                                                                                                                                                                                                                  |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Duplicate Connections        | Unchecked unless needed.                                                                                                                                                                                                                                                                                                                                                                  |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Dynamic IP                   | Checked unless seriously worried about laptops getting stolen in the middle of a VPN session or client connections being hijacked.                                                                                                                                                                                                                                                        |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Address Pool                 | Checked                                                                                                                                                                                                                                                                                                                                                                                   |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| DNS Default Domain           | Checked, enter the Active Directory domain name here                                                                                                                                                                                                                                                                                                                                      |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| DNS Servers                  | Checked, enter some Active Directory DNS server addresses here.                                                                                                                                                                                                                                                                                                                           |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| NTP Servers                  | If one of the DCs is acting as an NTP server, check and enter it here. Decent time keeping is important for AD communication but if there are no weird time problems or the client can maintain its own clock independently, it may remain unchecked.                                                                                                                                     |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| NetBIOS Options              | Unchecked. It's a security risk. Only check it if needed for legacy applications but check if they work without NetBIOS first; they probably do.                                                                                                                                                                                                                                          |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| WINS Servers                 | Unchecked unless needed.                                                                                                                                                                                                                                                                                                                                                                  |
+------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. image:: /_static/vpn/openvpn/radiusvpn_033.jpg
   :align: center

Configure the firewall
^^^^^^^^^^^^^^^^^^^^^^

Go to **Firewall > Rules**, **WAN** tab and click |fa-plus| to create a new
rule.

.. image:: /_static/vpn/openvpn/radiusvpn_207.jpg
   :align: center

Enter these values:

+--------------------------+-----------------------------------+
| Action                   | Pass                              |
+--------------------------+-----------------------------------+
| Disabled                 | not checked                       |
+--------------------------+-----------------------------------+
| Interface                | WAN                               |
+--------------------------+-----------------------------------+
| Protocol                 | UDP                               |
+--------------------------+-----------------------------------+
| Source                   | unchecked, any                    |
+--------------------------+-----------------------------------+
| Destination              | unchecked, WAN address            |
+--------------------------+-----------------------------------+
| Destination port range   | from OpenVPN to OpenVPN           |
+--------------------------+-----------------------------------+
| Log                      | only check when troubleshooting   |
+--------------------------+-----------------------------------+
| Description              | OpenVPN RADIUS                    |
+--------------------------+-----------------------------------+

.. image:: /_static/vpn/openvpn/radiusvpn_202.jpg
   :align: center

Click **Save** and the rules page will reload. Do not forget to click
**Apply Changes**.

.. image:: /_static/vpn/openvpn/radiusvpn_203.jpg
   :align: center

Create a Certificate
^^^^^^^^^^^^^^^^^^^^

A certificate must be created for each user that is going to use the VPN
system. In **Descriptive** and **Common Name**, enter the username the
user uses to log on to Active Directory. Strictly speaking **Descriptive
name** can be anything but usernames should be unique anyway.

Go to **System > Cert Manager** (not User Manager!), **Certificates**
tab and click |fa-plus|.

.. image:: /_static/vpn/openvpn/radiusvpn_102.jpg
   :align: center

Enter these values:

+-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Method                  | Create an internal Certificate                                                                                                                                                   |
+-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Descriptive name        | | [Username of the user that will be using the vpn connection]                                                                                                                   |
|                         | | In some cases this is case sensitive. I tend to stick to all lowercase for that reason. It doesn't really matter but keep it in mind if the connection can't be established.   |
+-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Certificate authority   | TestDomain VPN CA                                                                                                                                                                |
+-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Key length              | 2048                                                                                                                                                                             |
+-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Certificate Type        | User Certificate                                                                                                                                                                 |
+-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Lifetime                | | 3650 days                                                                                                                                                                      |
|                         | | Unless the user has a temporary account.                                                                                                                                       |
+-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Distinguished name      | Fill out the preferences here.                                                                                                                                                   |
+-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Common Name:            | [see Descriptive name]                                                                                                                                                           |
+-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. image:: /_static/vpn/openvpn/radiusvpn_104.jpg
   :align: center

Note the entry in the Certificate list.

.. image:: /_static/vpn/openvpn/radiusvpn_105.jpg
   :align: center

Install the OpenVPN Client Export Package
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Go to **System > Packages**, **Available Packages** tab.

.. image:: /_static/vpn/openvpn/radiusvpn_106.jpg
   :align: center

Scroll down to :doc:`OpenVPN Client Export Package
</vpn/openvpn/using-the-openvpn-client-export-package>` and click |fa-plus| on
the right.

.. image:: /_static/vpn/openvpn/radiusvpn_107.jpg
   :align: center

Confirm the selection and the package will be installed.

When it says **Installation completed** the installation is finished.

.. image:: /_static/vpn/openvpn/radiusvpn_108.jpg
   :align: center

Prepare the Windows package
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Go to **VPN > OpenVPN** and note that there is an extra tab called
**Client Export**. Click it.

.. image:: /_static/vpn/openvpn/radiusvpn_208.jpg
   :align: center

Enter these values:

+----------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Remote Access Server                                                             | VPN with RADIUS UDP:1194                                                                                                                                                                          |
+----------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Host Name Resolution                                                             | | - If WAN has a static IP, enter *Interface IP Address* here.                                                                                                                                    |
|                                                                                  | | - If there is a DNS address pointing to the firewall, enter *Installation hostname* here.                                                                                                       |
|                                                                                  |                                                                                                                                                                                                   |
|                                                                                  | Personally, I like to create a dedicated DNS entry for VPN connections called *vpn.example.com*. If IP addresses / ISP connections are moved around it is nice to have things set up modularly.   |
|                                                                                  |                                                                                                                                                                                                   |
|                                                                                  | If unsure, stick with *Interface IP Address* for now.                                                                                                                                             |
+----------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Use Microsoft Certificate Storage instead of local files                         | checked                                                                                                                                                                                           |
+----------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Use a password to protect the pkcs12 file contents or key in Viscosity bundle.   | checked; choose a random password here and save it for use when installing the certificate on the client.                                                                                         |
+----------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Use HTTP Proxy                                                                   | Unchecked unless needed.                                                                                                                                                                          |
+----------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Find the right username under **Certificate Name** and then in the
**Windows Installer** section, choose an appropriate installer for the
user's platform, such as **x64-win6** for a 64-bit installer for Windows
Vista and later.

.. image:: /_static/vpn/openvpn/radiusvpn_110.jpg
   :align: center

Get a package for each user.

On the Windows clients
----------------------

install the OpenVPN package
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Copy the downloaded Windows Installed to the client. It is named after
the tunnel configuration, for example *router-udp-1194-install.exe*.

Run the installer with all defaults. When selecting components, make
sure they are all checked (they are by default).

.. image:: /_static/vpn/openvpn/radiusvpn_112.jpg
   :align: center

The OpenVPN Configuration Setup will continue to install the
certificates.

.. image:: /_static/vpn/openvpn/radiusvpn-113-en.png
   :align: center

Stick to the defaults. When prompted for a password, enter the password
used when exporting the Windows Installer from the **Client Export**
tab.

.. image:: /_static/vpn/openvpn/radiusvpn-114-en.png
   :align: center

Have the wizard automatically select the archive.

.. image:: /_static/vpn/openvpn/radiusvpn-115-en.png
   :align: center

Change the cryptoapicert SUBJ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Open ``C:\Program Files\OpenVPN\config\config.ovpn`` or ``C:\Program
Files(x86)\OpenVPN\config\config.ovpn`` and change the line that says

    cryptoapicert "SUBJ:"

to

    cryptoapicert "SUBJ:username"

...replace ``username`` by the user's actual username.

This helps specifying which certificate OpenVPN should use in case certificates
have a naming conflict.

Using the Windows client
^^^^^^^^^^^^^^^^^^^^^^^^

Set the Windows Client to :doc:`run as Administrator </vpn/openvpn/troubleshooting-windows-openvpn-client-connectivity>`.

To use the client, double click the OpenVPN GUI icon on the Desktop.

.. image:: /_static/vpn/openvpn/radiusvpn_116.jpg
   :align: center

Windows will ask to confirm the execution. Confirm.

OpenVPN will start but that's not enough. Right-click the OpenVPN icon
in the taskbar and choose **Connect**.

.. image:: /_static/vpn/openvpn/radiusvpn_117.jpg
   :align: center

The user must now enter their username and password. This is only the
username part, without the domain. The password is the user's Active
Directory password.

.. image:: /_static/vpn/openvpn/radiusvpn-118-en.png
   :align: center

If all is well, OpenVPN will connect to the pfSense router and minimize
to the system tray.

.. image:: /_static/vpn/openvpn/radiusvpn_119.jpg
   :align: center

Right-click the system tray icon and choose **Disconnect** or **Close**
to either disconnect the tunnel or close the OpenVPN program altogether.

Tweaking the client
-------------------

Here are some tweaks I like to do on my client installations.

Change the name of the .ovpn file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When connecting to the firewall OpenVPN shows a balloon announcing that
the VPN is up. It contains a rather cryptic Windows Installer name, but
that can be changed to something more appropriate by renaming the
``.ovpn`` file in ``C:\Windows\Program Files\OpenVPN\config`` (or
``C:\Windows\Program Files(x86)\OpenVPN\config``) to whatever name the
balloon should show.

.. image:: /_static/vpn/openvpn/radiusvpn_122.jpg
   :align: center

(*is nu verbonden* is dutch for *is now connected*.)

Edit the shortcut to connect directly
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The shortcut to OpenVPN GUI can be edited to directly connect to a
firewall instead of first starting OpenVPN and then starting the
connection by right-clicking the shortcut and adding to the **Target**
field:

    --connect "Headquarters.ovpn"

...if *Headquarters.ovpn* is the name of the *.ovpn* file.

.. image:: /_static/vpn/openvpn/radiusvpn_206.jpg
   :align: center

The user will still need to enter their password but it does save a step
in the process.

Edit more settings
^^^^^^^^^^^^^^^^^^

More information on automation, customization and registry tweaks are
available in this text document: http://openvpn.se/install.txt

Troubleshooting
---------------

If something doesn't work, here are some pointers for troubleshooting:

-  The username may be case sensitive.
-  Use the fine pfSense logging system under **Status** > **System logs**
   > **OpenVPN**.
-  Ask questions in the pfSense forum.
-  Windows 7 sometimes adds a *Microsoft Virtual WiFi Miniport Adapter*.
   Disabling this sometimes solves vague connection problems where there
   should be none.
-  Is the subnet unique? Perhaps the user is in a subnet that is the
   same as the virtual or corporate subnet.
-  Certificate problems? Check **certmgr.msc**. Perhaps an old
   certificate is blocking the installation of a new certificate.
-  Client getting disconnected? Check the user's wifi connection. No
   wifi=no internet=no vpn.
-  Check if the domain controller allows UDP ports 1812 and 1813
   throughout the firewall. Adding the *Network Policy and Access
   Services* role and configuring a RADIUS client should automatically
   have entered these rules in the server's firewall. They are called
   *Network Policy Server (RADIUS Accounting - UDP-In)* and *Network
   Policy Server (RADIUS Authentication - UDP-In)*. Note that this is
   about the firewall on the domain controller, not the firewall on
   pfSense!
