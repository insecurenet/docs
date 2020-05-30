2.5.0 New Features and Changes
==============================

pfSense® software version 2.5.0 brings a major OS version upgrade, OpenSSL
upgrades, PHP and Python upgrades, and numerous bug fixes.

.. warning:: The original plan was to include a RESTCONF API in pfSense version
   2.5.0, which for security reasons would have required hardware AES-NI or
   equivalent support. Plans have since changed, and pfSense 2.5.0 does not
   contain the planned RESTCONF API, thus **pfSense version 2.5.0 WILL NOT
   require AES-NI**.

.. tip:: For those who have not yet updated to 2.4.4-p3 or 2.4.4, consult
   the :doc:`previous release notes <index>` and `blog posts for those releases
   <https://www.netgate.com/blog/category.html#releases>`__ to read all
   important information and warnings before proceeding.

Operating System / Architecture changes
---------------------------------------

* Base OS upgraded to FreeBSD **12.0-RELEASE-p10**
* OpenSSL upgraded to **1.1.1a-freebsd**
* PHP upgraded to **7.3** `#9365 <https://redmine.pfsense.org/issues/9365>`__
* Python upgraded to **3.6** `#9360 <https://redmine.pfsense.org/issues/9360>`__

Security / Errata
-----------------

* Deprecated the built-in relayd Load Balancer `#9386 <https://redmine.pfsense.org/issues/9386>`__

  * ``relayd`` does not function with OpenSSL 1.1.x
  * The ``relayd`` FreeBSD port has been changed to require libressl -- There is no apparent sign of work to make it compatible with OpenSSL 1.1.x
  * The HAProxy package may be used in its place; It is a much more robust and more feature-complete load balancer and reverse proxy
  * For more information on implementing HAProxy, see :doc:`../packages/haproxy-package` and the `Hangout <https://www.netgate.com/resources/videos/server-load-balancing-on-pfsense-24.html>`_

.. warning:: See the `FreeBSD 12.0 Release Notes <https://www.freebsd.org/releases/12.0R/relnotes.html#drivers-network>`_
   for information on deprecated hardware drivers that may impact firewalls
   upgrading to pfSense version 2.5.0. Some of these were renamed or folded into
   other drivers, others have been removed, and more are slated for removal in
   FreeBSD 13 in the future.

Known Issues
------------

* During development of pfSense version 2.5.0, there is a significant chance
  that packages will be unstable until closer to the release. Most of this is
  due to OpenSSL changes. This will stabilize as development progresses.

Aliases/Tables
--------------

* Fixed URL-based Alias only storing last-most entry in the configuration `#9074 <https://redmine.pfsense.org/issues/9074>`__
* Fixed an issue with PF tables remaining active after they had been deleted `#9790 <https://redmine.pfsense.org/issues/9790>`__
* Added support for URL/URL Table aliases using IDN hostnames `#10321 <https://redmine.pfsense.org/issues/10321>`__

Authentication
--------------

* Set RADIUS NAS Identifier to include ``webConfigurator`` and the firewall hostname when logging in the GUI `#9209 <https://redmine.pfsense.org/issues/9209>`__
* Added LDAP extended query for groups in RFC2307 containers `#9527 <https://redmine.pfsense.org/issues/9527>`__

Backup/Restore
--------------

* Changed ``crypt_data()`` to use stronger key derivation `#9421 <https://redmine.pfsense.org/issues/9421>`__
* Updated ``crypt_data()`` syntax for OpenSSL 1.1.x `#9420 <https://redmine.pfsense.org/issues/9420>`__ `#10178 <https://redmine.pfsense.org/issues/10178>`__
* Disabled AutoConfigBackup manual backups when AutoConfigBackup is disabled `#9785 <https://redmine.pfsense.org/issues/9785>`__
* Improved error handling when attempting to restore encrypted and otherwise invalid configurations which result in errors (e.g. wrong encryption passphrase, malformed XML) `#10179 <https://redmine.pfsense.org/issues/10179>`__

Captive Portal
--------------

* Changed Captive Portal vouchers to use ``phpseclib`` so it can generate keys natively in PHP, and to work around OpenSSL deprecating key sizes needed for vouchers `#9443 <https://redmine.pfsense.org/issues/9443>`__
* Added ``trim()`` to the submitted username, so that spaces before/after in input do not cause authentication errors `#9274 <https://redmine.pfsense.org/issues/9274>`__
* Optimized Captive Portal authentication attempts when using multiple authentication servers `#9255 <https://redmine.pfsense.org/issues/9255>`__
* Fixed Captive Portal session timeout values for RADIUS users who do not have a timeout returned from the server `#9208 <https://redmine.pfsense.org/issues/9208>`__
* Changed Captive Portal so that users no longer get disconnected when changes are made to Captive Portal settings `#8616 <https://redmine.pfsense.org/issues/8616>`__
* Added an option so that Captive Portals may choose to remove or retain logins across reboot `#5644 <https://redmine.pfsense.org/issues/5644>`__

Certificates
------------

* Fixed OCSP stapling detection for OpenSSL 1.1.x `#9408 <https://redmine.pfsense.org/issues/9408>`__
* Fixed GUI detection of revoked status for certificates issued and revoked by an intermediate CA `#9924 <https://redmine.pfsense.org/issues/9924>`__
* Removed PKCS#12 export links for entries which cannot be exported in that format (e.g. no private key) `#10284 <https://redmine.pfsense.org/issues/10284>`__
* Added an option to globally trust local CA manager entries `#4068 <https://redmine.pfsense.org/issues/4068>`__
* Added support for randomized certificate serial numbers when creating or signing certificates with local internal CAs `#9883 <https://redmine.pfsense.org/issues/9883>`__
* Added validation for CA/CRL serial numbers `#9883 <https://redmine.pfsense.org/issues/9883>`__ `#9869 <https://redmine.pfsense.org/issues/9869>`__
* Added support for importing ECDSA keys in certificates and when completing signing requests `#9745 <https://redmine.pfsense.org/issues/9745>`__
* Added support for creating and signing certificates using ECDSA keys `#9843 <https://redmine.pfsense.org/issues/9843>`__
* Added detailed certificate information block to the CA list, using code shared with the Certificate list `#9856 <https://redmine.pfsense.org/issues/9856>`__
* Added Certificate Lifetime to certificate information block `#7332 <https://redmine.pfsense.org/issues/7332>`__
* Added CA validity checks when attempting to pre-fill certificate fields from a CA `#3956 <https://redmine.pfsense.org/issues/3956>`__
* Added a daily certificate expiration check and notice, with settings to control its behavior and notifications (Default: 27 days) `#7332 <https://redmine.pfsense.org/issues/7332>`__
* Added functionality to allow importing certificates without private keys (e.g. PKCS#11) `#9834 <https://redmine.pfsense.org/issues/9834>`__
* Added CA/Certificate renewal functionality `#9842 <https://redmine.pfsense.org/issues/9842>`__

  * This allows a CA or certificate to be renewed using its current settings (or a more secure profile), replacing the entry with a fresh one, and optionally retaining the existing key.

* Added an "Edit" screen for Certificate entries
    * This view allows editing the Certificate **Descriptive name** field `#7861 <https://redmine.pfsense.org/issues/7861>`__
    * This view also adds a (not stored) password field and buttons for exporting encrypted private keys and PKCS#12 archives `#1192 <https://redmine.pfsense.org/issues/1192>`__

* Improved default GUI certificate strength and handling of weak values `#9825 <https://redmine.pfsense.org/issues/9825>`__
    * Reduced the default GUI web server certificate lifetime to 398 days to prevent errors on Apple platforms `#9825 <https://redmine.pfsense.org/issues/9825>`__
    * Added notes on CA/Cert pages about using potentially insecure parameter choices
    * Added visible warnings on CA/Cert pages if parameters are known to be insecure or not recommended

* Revamped CRL management to be easier to use and more capable
    * Added the ability to revoke certificates by serial number `#9869 <https://redmine.pfsense.org/issues/9869>`__
    * Added the ability to revoke multiple entries at a time `#3258 <https://redmine.pfsense.org/issues/3258>`__
    * Decluttered the main CRL list screen
    * Moved to a single CRL create control to the bottom under the list rather than multiple buttons

* Optimized CA/Cert/CRL code in various ways, including:
    * Actions are now performed by ``refid`` rather than array index, which is more accurate and not as prone to being affected by parallel changes
    * Improved configuration change descriptions as shown in the GUI and configuration history/backups
    * Miscellaneous style and code re-use improvements
    * Changed CA/Cert date calculations to use a more accurate method, which ensures accuracy on ARM past the 2038 date barrier `#9899 <https://redmine.pfsense.org/issues/9899>`__

Dashboard
---------

* Added PPP uptime to the Dashboard Interfaces Widget `#9426 <https://redmine.pfsense.org/issues/9426>`__

DHCP
----

* Fixed handling of spaces in DHCP lease hostnames by ``dhcpleases`` `#9758 <https://redmine.pfsense.org/issues/9758>`__
* Fixed DHCP leases hostname parsing problems which prevented some hostnames from being displayed in the GUI `#3500 <https://redmine.pfsense.org/issues/3500>`__
* Added OMAPI settings to the DHCP Server `#7304 <https://redmine.pfsense.org/issues/7304>`__
* Added options to disable pushing IPv6 DNS servers to clients via DHCP6 `#9302 <https://redmine.pfsense.org/issues/9302>`__
* Fixed DHCPv6 domain search list `#10200 <https://redmine.pfsense.org/issues/10200>`__
* Increased number of NTP servers sent via DHCP to 3 `#9661 <https://redmine.pfsense.org/issues/9661>`__
* Added an option to prevent known DHCP clients from obtaining addresses on any interface (e.g. known clients may only obtain an address from the interface where the entry is defined) `#1605 <https://redmine.pfsense.org/issues/1605>`__
* Added count of static mappings to list when editing DHCP settings for an interface `#9282 <https://redmine.pfsense.org/issues/9282>`__
* Fixed validation to allow omission of DHCPv6 range for use with stateless DHCP `#9596 <https://redmine.pfsense.org/issues/9596>`__
* Fixed handling of client identifiers on static mappings containing double quotes `#10295 <https://redmine.pfsense.org/issues/10295>`__

Diagnostics
-----------

* Added Reroot and Reboot with Filesystem Check options to GUI Reboot page `#9771 <https://redmine.pfsense.org/issues/9771>`__
* Added option to control wait time between ICMP echo request (ping) packets ``diag_ping.php`` `#9862 <https://redmine.pfsense.org/issues/9862>`__

DNS
---

* Added TCP_RFC7413 in kernel, required for the BIND package `#7293 <https://redmine.pfsense.org/issues/7293>`__
* Added IPv6 OpenVPN client addresses resolution to the DNS Resolver `#8624 <https://redmine.pfsense.org/issues/8624>`__
* Enhanced eDNS buffer size default behavior and options in the DNS Resolver `#10293 <https://redmine.pfsense.org/issues/10293>`__
* Added DNS64 options to the DNS Resolver `#10274 <https://redmine.pfsense.org/issues/10274>`__

Dynamic DNS
-----------

* Fixed Dynamic DNS Dashboard Widget address parsing for entries with split hostname/domain (e.g. Namecheap) `#9564 <https://redmine.pfsense.org/issues/9564>`__
* Added support for new CloudFlare Dynamic DNS API tokens `#9639 <https://redmine.pfsense.org/issues/9639>`__
* Added IPv6 support to No-IP Dynamic DNS `#10256 <https://redmine.pfsense.org/issues/10256>`__
* Fixed issues with Hover Dynamic DNS `#10241 <https://redmine.pfsense.org/issues/10241>`__

Interfaces
----------

* Fixed issues with PPPoE over a VLAN failing to reconnect `#9148 <https://redmine.pfsense.org/issues/9148>`__
* Changed the way interface VLAN support is detected so it does not rely on the VLANMTU flag `#9548 <https://redmine.pfsense.org/issues/9548>`__
* Added a PHP shell playback script ``restartallwan`` which restarts all WAN-type interfaces `#9688 <https://redmine.pfsense.org/issues/9688>`__
* Changed assignment of the ``fe80::1:1`` default IPv6 link-local LAN address so it does not remove existing entries, which could cause problems such as Unbound failing to start `#9998 <https://redmine.pfsense.org/issues/9998>`__
* Added automatic MTU adjustment for GRE interfaces using IPsec as a transport `#10222 <https://redmine.pfsense.org/issues/10222>`__
* Fixed SLAAC interface selection when using IPv6 on a link which also uses PPP `#9324 <https://redmine.pfsense.org/issues/9324>`__
* Enabled selection of QinQ interfaces for use with PPP `#9472 <https://redmine.pfsense.org/issues/9472>`__
* Added GUI interface descriptions to Operating System interfaces `#1557 <https://redmine.pfsense.org/issues/1557>`__

IPsec
-----

* Added 25519 curve-based IPsec DH and PFS groups 31 and 32 `#9531 <https://redmine.pfsense.org/issues/9531>`__
* Enabled the strongSwan PKCS#11 plugin `#6775 <https://redmine.pfsense.org/issues/6775>`__
* Added support for ECDSA certificates to IPsec for IKE `#4991 <https://redmine.pfsense.org/issues/4991>`__
* Renamed IPsec "RSA" options to "Certificate" since both RSA and ECDSA certificates are now supported, and it is also easier for users to recognize `#9903 <https://redmine.pfsense.org/issues/9903>`__
* Converted IPsec configuration code from ``ipsec.conf`` ``ipsec``/``stroke`` style to ``swanctl.conf`` ``swanctl``/``vici`` style `#9603 <https://redmine.pfsense.org/issues/9603>`__

  * Split up much of the single large IPsec configuration function into multiple functions as appropriate.
  * Optimized code along the way, including reducing code duplication and finding ways to generalize functions to support future expansion.
  * For IKEv1 and IKEv2 with Split Connections enabled, P2 settings are properly respected for each individual P2, such as separate encryption algorithms `#6263 <https://redmine.pfsense.org/issues/6263>`__

    * **N.B.:** In rare cases this may expose a previous misconfiguration which allowed a Phase 2 SA to connect with improper settings, for example if a required encryption algorithm was enabled on one P2 but not another.

  * New GUI option under **VPN > IPsec**, **Mobile Clients** tab to enable RADIUS Accounting which was previously on by default. This is now disabled by default as RADIUS accounting data will be sent for every tunnel, not only mobile clients, and if the accounting data fails to reach the RADIUS server, tunnels may be disconnected.
  * Additional developer & advanced user notes:

    * For those who may have scripts which touched files in ``/var/etc/ipsec``, note that the structure of this directory has changed to the new `swanctl layout <https://wiki.strongswan.org/projects/strongswan/wiki/Swanctldirectory>`__.
    * Any usage of ``/usr/local/sbin/ipsec`` or the stroke plugin must also be changed to ``/usr/local/sbin/swanctl`` and VICI. Note that some commands have no direct equivalents, but the same or better information is available in other ways.
    * IPsec start/stop/reload functions now use ``/usr/local/sbin/strongswanrc``
    * IPsec-related functions were converged into ``ipsec.inc``, removed from ``vpn.inc``, and renamed from ``vpn_ipsec_<name>`` to ``ipsec_<name>``
  * Reworked how reauthentication and rekey behavior functions, giving more control to the user compared to previous options `#9983 <https://redmine.pfsense.org/issues/9983>`__
* Reformatted ``status_ipsec.php`` to include more available information (rekey timer, encryption key size, IKE SPIs, ports) `#9979 <https://redmine.pfsense.org/issues/9979>`__
* Added support for PKCS#11 authentication (e.g. hardware tokens such as Yubikey) for IPsec `#9878 <https://redmine.pfsense.org/issues/9878>`__
* Fixed disabling an IPsec P1 entry with a VTI P2 when an interface assignment does not exist `#10190 <https://redmine.pfsense.org/issues/10190>`__
* Fixed usage of Hash Algorithm on child ESP/AH proposals using AEAD ciphers `#9726 <https://redmine.pfsense.org/issues/9726>`__
* Added support for IPsec remote gateway entries using FQDNs which resolve to IPv6 addresses `#9405 <https://redmine.pfsense.org/issues/9405>`__
* Added a warning against using DH group 5 `#10221 <https://redmine.pfsense.org/issues/10221>`__
* Added manual selection of Pseudo-Random Function (PRF) for use with AEAD ciphers `#9309 <https://redmine.pfsense.org/issues/9309>`__
* Added support for using per-user addresses from RADIUS and falling back to a local pool otherwise `#8160 <https://redmine.pfsense.org/issues/8160>`__
* Added an option which allows multiple tunnels to use the same remote peer in certain situations (read warnings on the option before use) `#10214 <https://redmine.pfsense.org/issues/10214>`__
* Fixed handling of automatic outbound NAT and per-user IPsec client address settings `#9320 <https://redmine.pfsense.org/issues/9320>`__

L2TP
----

* Allow L2TP usernames to include ``@`` `#9828 <https://redmine.pfsense.org/issues/9828>`__
* Changed L2TP to not restart the service when updating users, since it is not required `#4866 <https://redmine.pfsense.org/issues/4866>`__

Logging
-------

* Changed system logging to use plain text logging and log rotation, the old binary clog format has been deprecated `#8350 <https://redmine.pfsense.org/issues/8350>`__
* Updated firewall log daemon to match data structure changes for FreeBSD 12.x `#9411 <https://redmine.pfsense.org/issues/9411>`__
* Updated firewall log parsing to match new format of logs in FreeBSD 12.x `#9415 <https://redmine.pfsense.org/issues/9415>`__
* Updated default log size (512k + rotated copies), default lines to display (500, was 50), and max line limits (200k, up from 2k) `#9734 <https://redmine.pfsense.org/issues/9734>`__
* Added log tabs for nginx, userlog, utx/lastlog, and some other previously hidden logs `#9714 <https://redmine.pfsense.org/issues/9714>`__
* Relocated Package Logs into a tab under System Logs and standardized display/filtering of package logs `#9714 <https://redmine.pfsense.org/issues/9714>`__
* Added GUI options to control log rotation `#9711 <https://redmine.pfsense.org/issues/9711>`__
* Added code for packages to set their own log rotation parameters `#9712 <https://redmine.pfsense.org/issues/9712>`__
* Removed the redundant ``nginx-error.log`` file `#7198 <https://redmine.pfsense.org/issues/7198>`__
* Fixed some instances where logs were mixed into the wrong log files/tabs (Captive Portal/DHCP/squid/php/others) `#1375 <https://redmine.pfsense.org/issues/1375>`__
* Reorganized/restructured several log tabs `#9714 <https://redmine.pfsense.org/issues/9714>`__
* Added a dedicated authentication log `#9754 <https://redmine.pfsense.org/issues/9754>`__
* Added an option for RFC 5424 format log messages which have RFC 3339 timestamps `#9808 <https://redmine.pfsense.org/issues/9808>`__

Notifications
-------------

* Deprecated & Removed Growl Notifications `#8821 <https://redmine.pfsense.org/issues/8821>`__
* Added a daily certificate expiration notification with settings to control its behavior `#7332 <https://redmine.pfsense.org/issues/7332>`__
* Fixed input validation of SMTP notification settings `#8522 <https://redmine.pfsense.org/issues/8522>`__
* Fixed handling of the option to disable SMTP server certificate validation `#10317 <https://redmine.pfsense.org/issues/10317>`__

NTPD
----

* Added GUI options for NTP sync/poll intervals `#6787 <https://redmine.pfsense.org/issues/6787>`__
* Added validation to prevent using ``noselect`` and ``noserve`` with pools `#9830 <https://redmine.pfsense.org/issues/9830>`__
* Added feature to automatically detect GPS baud rate `#7284 <https://redmine.pfsense.org/issues/7284>`__
* Fixed status and widget display of long hostnames and stratum `#10307 <https://redmine.pfsense.org/issues/10307>`__
* Fixed handling of the checkbox options on NTP servers `#10276 <https://redmine.pfsense.org/issues/10276>`__

OpenVPN
-------

* Updated OpenVPN local auth to handle changes in fcgicli output `#9460 <https://redmine.pfsense.org/issues/9460>`__
* Added connection count to OpenVPN status and widget `#9788 <https://redmine.pfsense.org/issues/9788>`__
* Enabled the OpenVPN x509-alt-username build option `#9884 <https://redmine.pfsense.org/issues/9884>`__
* Added an option to enable/disable OpenVPN ``username-as-common-name`` `#8289 <https://redmine.pfsense.org/issues/8289>`__
* Restructured the OpenVPN settings directory layout

  * Changed from ``/var/etc/openvpn[-csc]/<mode><id>.<file>`` to ``/var/etc/openvpn/<mode><id>/<x>``

    * This keeps all settings for each client and server in a clean structure

* Moved to ``CApath`` style CA structure for OpenVPN CA/CRL usage `#9915 <https://redmine.pfsense.org/issues/9915>`__
* Added support for OCSP verification of client certificates `#7767 <https://redmine.pfsense.org/issues/7767>`__
* Fixed a potential race condition in OpenVPN client ACLs obtained via RADIUS `#9206 <https://redmine.pfsense.org/issues/9206>`__
* Added support for more protocols (IP, ICMP), ports, and a template variable (``{clientip}``) in OpenVPN client ACLs obtained via RADIUS `#9206 <https://redmine.pfsense.org/issues/9206>`__

Routing / Gateways
------------------

* Enabled the RADIX_MPATH kernel option for multi-path routing `#9544 <https://redmine.pfsense.org/issues/9544>`__
* Fixed automatic static routes set for DNS gateway bindings not being removed when no longer necessary `#8922 <https://redmine.pfsense.org/issues/8922>`__
* Fixed route removal to always specify the gateway `#10001 <https://redmine.pfsense.org/issues/10001>`__
* Added validation to prevent using descriptions on interfaces which would cause gateway names to exceeded the maximum allowed length `#9401 <https://redmine.pfsense.org/issues/9401>`__
* Added support for obtaining a gateway via DHCP which is outside of the interface subnet `#7380 <https://redmine.pfsense.org/issues/7380>`__
* Fixed gateway names when created at the console to match the same naming convention used in the GUI `#10264 <https://redmine.pfsense.org/issues/10264>`__

Rules / NAT
-----------

* Added the ability to configure negated tagging, to match packets which do not not contain a given tag `#10186 <https://redmine.pfsense.org/issues/10186>`__
* Excluded disabled IPsec P2 networks from automatic ``vpn_networks`` table `#7622 <https://redmine.pfsense.org/issues/7622>`__
* Fixed handling of special characters in schedule descriptions `#10305 <https://redmine.pfsense.org/issues/10305>`__

Traffic Shaper / Limiters
-------------------------

* Removed bogus additional warning dialog when deleting traffic shaper entries `#9334 <https://redmine.pfsense.org/issues/9334>`__

Translations
------------

* Added Italian translation `#9716 <https://redmine.pfsense.org/issues/9716>`__

Upgrade / Installation
----------------------

* Fixed issues with checking for updates from the GUI behind a proxy with authentication `#9478 <https://redmine.pfsense.org/issues/9478>`__
* Created separate **Auto (UFS) UEFI** and **Auto (UFS) BIOS** installation options to avoid problems on hardware which boots differently on USB and non-USB disks `#8638 <https://redmine.pfsense.org/issues/8638>`__

User Manager / Privileges
-------------------------

* Added menu entry for User Password Manager if the user does not have permission to reach the User Manager `#9428 <https://redmine.pfsense.org/issues/9428>`__
* Improved consistency of SSL/TLS references in LDAP authentication servers `#10172 <https://redmine.pfsense.org/issues/10172>`__

Web Interface
-------------

* Increased the number of colors available for the login screen `#9706 <https://redmine.pfsense.org/issues/9706>`__
* Added TLS 1.3 to GUI and Captive Portal web server configuration, and removed older versions (TLS 1.0 removed from Captive Portal, TLS 1.1 removed from GUI) `#9607 <https://redmine.pfsense.org/issues/9607>`__
* Fixed empty lines in various forms throughout the GUI `#9449 <https://redmine.pfsense.org/issues/9449>`__
* Improved validation of FQDNs `#9023 <https://redmine.pfsense.org/issues/9023>`__
* Added ``poly1305-chacha20`` to ``nginx`` cipher list `#9896 <https://redmine.pfsense.org/issues/9896>`__
* Added input validation for IGMP Proxy settings `#7163 <https://redmine.pfsense.org/issues/7163>`__
* Improved behavior of the GUI when there is no WAN connectivity / no working DNS resolution `#8987 <https://redmine.pfsense.org/issues/8987>`__

Wireless
--------

* Added support for the ``athp(4)`` wireless interface driver `#9538 <https://redmine.pfsense.org/issues/9538>`__ `#9600 <https://redmine.pfsense.org/issues/9600>`__

Development
-----------

* Added a "periodic" style framework to allow for daily/weekly/monthly tasks from the base system or packages by way of plugin calls `#7332 <https://redmine.pfsense.org/issues/7332>`__
* Added a central file download function for internal use throughout the GUI

XMLRPC
------

* Added option to synchronize changes for the account used for XMLRPC sync `#9622 <https://redmine.pfsense.org/issues/9622>`__
* Fixed handling of IPv6 CARP VIP addresses when they were specified with non-significant zeroes `#6579 <https://redmine.pfsense.org/issues/6579>`__
