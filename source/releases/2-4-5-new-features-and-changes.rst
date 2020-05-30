2.4.5 New Features and Changes
==============================

pfSense® software version 2.4.5 contains a variety of bug fixes and maintenance
updates.

.. warning:: **Proceed with caution when upgrading pfSense software while
   COVID-19 travel restrictions are in effect.**

   During this time of travel limitations, remote upgrades of pfSense software
   should be carefully considered, and avoided where possible. Travel
   restrictions may complicate any repair of any issue, including
   hardware-related issues that render the system unreachable. Should these
   issues require onsite physical access to remedy, repair of the issue may not
   be possible while travel restrictions related to COVID-19 are in effect.

.. tip:: For those who have not yet updated to 2.4.4-p3 or 2.4.4, consult
   the :doc:`previous release notes <index>` and `blog posts for those releases
   <https://www.netgate.com/blog/category.html#releases>`__ to read all
   important information and warnings before proceeding.

Operating System / Architecture changes
---------------------------------------

* Base OS upgraded to FreeBSD `11.3-STABLE@r357046 <https://www.freebsd.org/doc/handbook/current-stable.html#stable>`__
* PHP upgraded to 7.2.29

Security / Errata
-----------------

* Fixed dependency issues with ``pfSense-upgrade`` which may have caused it not to update itself properly `#10303 <https://redmine.pfsense.org/issues/10303>`__

  .. tip:: If the update check fails, or the update does not complete, run ``pkg install -y pfSense-upgrade`` to ensure that ``pfSense-upgrade`` is present.

* Added encoding to the hostname in ``services_acb.php`` `#9584 <https://redmine.pfsense.org/issues/9584>`__
* Added encoding to error output in ``services_captiveportal_mac.php`` `#9609 <https://redmine.pfsense.org/issues/9609>`__
* Improved Picture Widget input validation `#9610 <https://redmine.pfsense.org/issues/9610>`__ `#9731 <https://redmine.pfsense.org/issues/9731>`__ `#9804 <https://redmine.pfsense.org/issues/9804>`__
* Added a ``fsck`` run with ``-z`` for ``UFS`` filesystems on upgrade to address FreeBSD-SA-19:10.ufs `#9612 <https://redmine.pfsense.org/issues/9612>`__
* Fixed format of XMLRPC auth error to match GUI auth error `#9782 <https://redmine.pfsense.org/issues/9782>`__
* Added a custom CSRF Error page with warnings and confirmation prompts before resubmitting potentially harmful data `#9799 <https://redmine.pfsense.org/issues/9799>`__
* Fixed Status_Monitoring ``rrd_fetch_json.php`` error encoding `#9601 <https://redmine.pfsense.org/issues/9601>`__
* Fixed encoding of the user full name on ``system_usermanager_addprivs.php`` `#10324 <https://redmine.pfsense.org/issues/10324>`__
* Fixed input validation and output encoding of host on ``diag_ping.php`` `#10355 <https://redmine.pfsense.org/issues/10355>`__

* Addressed FreeBSD Security Advisories & Errata Notices

  * `FreeBSD-SA-20:05.if_oce_ioctl <https://www.freebsd.org/security/advisories/FreeBSD-SA-20:05.if_oce_ioctl.asc>`__
  * `FreeBSD-SA-20:04.tcp       <https://www.freebsd.org/security/advisories/FreeBSD-SA-20:04.tcp.asc>`__
  * `FreeBSD-SA-19:24.mqueuefs  <https://security.freebsd.org/advisories/FreeBSD-SA-19:24.mqueuefs.asc>`__
  * `FreeBSD-SA-19:23.midi      <https://security.freebsd.org/advisories/FreeBSD-SA-19:23.midi.asc>`__
  * `FreeBSD-SA-19:22.mbuf      <https://security.freebsd.org/advisories/FreeBSD-SA-19:22.mbuf.asc>`__
  * `FreeBSD-SA-19:21.bhyve     <https://security.freebsd.org/advisories/FreeBSD-SA-19:21.bhyve.asc>`__
  * `FreeBSD-SA-19:20.bsnmp     <https://security.freebsd.org/advisories/FreeBSD-SA-19:20.bsnmp.asc>`__
  * `FreeBSD-SA-19:19.mldv2     <https://security.freebsd.org/advisories/FreeBSD-SA-19:19.mldv2.asc>`__
  * `FreeBSD-SA-19:18.bzip2     <https://security.freebsd.org/advisories/FreeBSD-SA-19:18.bzip2.asc>`__
  * `FreeBSD-SA-19:17.fd        <https://security.freebsd.org/advisories/FreeBSD-SA-19:17.fd.asc>`__
  * `FreeBSD-SA-19:16.bhyve     <https://security.freebsd.org/advisories/FreeBSD-SA-19:16.bhyve.asc>`__
  * `FreeBSD-SA-19:15.mqueuefs  <https://security.freebsd.org/advisories/FreeBSD-SA-19:15.mqueuefs.asc>`__
  * `FreeBSD-SA-19:14.freebsd32 <https://security.freebsd.org/advisories/FreeBSD-SA-19:14.freebsd32.asc>`__
  * `FreeBSD-SA-19:13.pts       <https://security.freebsd.org/advisories/FreeBSD-SA-19:13.pts.asc>`__
  * `FreeBSD-SA-19:12.telnet    <https://security.freebsd.org/advisories/FreeBSD-SA-19:12.telnet.asc>`__
  * `FreeBSD-SA-19:11.cd_ioctl  <https://security.freebsd.org/advisories/FreeBSD-SA-19:11.cd_ioctl.asc>`__
  * `FreeBSD-SA-19:10.ufs       <https://security.freebsd.org/advisories/FreeBSD-SA-19:10.ufs.asc>`__
  * `FreeBSD-SA-19:09.iconv     <https://security.freebsd.org/advisories/FreeBSD-SA-19:09.iconv.asc>`__
  * `FreeBSD-SA-19:08.rack      <https://security.freebsd.org/advisories/FreeBSD-SA-19:08.rack.asc>`__
  * `FreeBSD-EN-20:06.ipv6      <https://www.freebsd.org/security/advisories/FreeBSD-EN-20:06.ipv6.asc>`__
  * `FreeBSD-EN-20:04.pfctl     <https://www.freebsd.org/security/advisories/FreeBSD-EN-20:04.pfctl.asc>`__
  * `FreeBSD-EN-19:18.tzdata    <https://security.freebsd.org/advisories/FreeBSD-EN-19:18.tzdata.asc>`__
  * `FreeBSD-EN-19:17.ipfw      <https://security.freebsd.org/advisories/FreeBSD-EN-19:17.ipfw.asc>`__
  * `FreeBSD-EN-19:16.bhyve     <https://security.freebsd.org/advisories/FreeBSD-EN-19:16.bhyve.asc>`__
  * `FreeBSD-EN-19:15.libunwind <https://security.freebsd.org/advisories/FreeBSD-EN-19:15.libunwind.asc>`__
  * `FreeBSD-EN-19:14.epoch     <https://security.freebsd.org/advisories/FreeBSD-EN-19:14.epoch.asc>`__
  * `FreeBSD-EN-19:13.mds       <https://security.freebsd.org/advisories/FreeBSD-EN-19:13.mds.asc>`__
  * `FreeBSD-EN-19:12.tzdata    <https://security.freebsd.org/advisories/FreeBSD-EN-19:12.tzdata.asc>`__
  * `FreeBSD-EN-19:11.net       <https://security.freebsd.org/advisories/FreeBSD-EN-19:11.net.asc>`__

Aliases/Tables
--------------

* Fixed an issue when resolving FQDN entries in aliases where some entries could be missing `#9296 <https://redmine.pfsense.org/issues/9296>`__
* Improved URL Table aliases to support FQDNs which return muliple entries `#8531 <https://redmine.pfsense.org/issues/8531>`__
* Added a function to download the contents of an individual alias `#9816 <https://redmine.pfsense.org/issues/9816>`__

Authentication
--------------

* Added exception handling to authentication attempts `#9150 <https://redmine.pfsense.org/issues/9150>`__

Backup/Restore
--------------

* Added a special string (``NoReMoTeBaCkUp``) that when used in ``write_config()`` descriptions will prevent a remote backup `#9693 <https://redmine.pfsense.org/issues/9693>`__
* Removed legacy AutoConfigBackup options (there were no more active accounts using the retired legacy service) `#9687 <https://redmine.pfsense.org/issues/9687>`__ `#9785 <https://redmine.pfsense.org/issues/9785>`__
* Added CDATA protection to the ``encryption_password`` XML tag, which allows international characters to be used in that field `#7186 <https://redmine.pfsense.org/issues/7186>`__
* Added CDATA escape to more auth-related fields `#9327 <https://redmine.pfsense.org/issues/9327>`__
* Ensured that ``kern.cam.boot_delay`` is set for new installations and upgrades so that USB devices are properly initialized in time for configuration restore in the installer and ECL to function `#9533 <https://redmine.pfsense.org/issues/9533>`__

Captive Portal
--------------

* Fixed Captive Portal vouchers shortcut links `#9722 <https://redmine.pfsense.org/issues/9722>`__
* Changed Captive Portal redirect page selection order `#9819 <https://redmine.pfsense.org/issues/9819>`__
* Fixed a rare and intermittent issue where users could encounter an ``nginx`` error when restarting Captive Portal instances `#10159 <https://redmine.pfsense.org/issues/10159>`__

Certificates
------------

* Added sorting and search/filtering to Certificate Authority & Certificate manager `#9412 <https://redmine.pfsense.org/issues/9412>`__
* Corrected wording of CA/Cert CN input validation `#9234 <https://redmine.pfsense.org/issues/9234>`__
* Fixed certificate Descriptive Name field behavior when adding a user certificate `#9719 <https://redmine.pfsense.org/issues/9719>`__
* Added ``clientAuth`` EKU to Server type certificates `#9868 <https://redmine.pfsense.org/issues/9868>`__
* Reduced the default GUI web server certificate lifetime to 398 days to prevent errors on Apple platforms `#9825 <https://redmine.pfsense.org/issues/9825>`__

Dashboard
---------

* Added option to disable PTI display in System Information widget `#9323 <https://redmine.pfsense.org/issues/9323>`__

DHCP
----

* Fixed incorrect expansion of Dynamic DNS advanced options on the DHCPv6 Server page `#9448 <https://redmine.pfsense.org/issues/9448>`__
* Changed DHCP relay backend code to determine and specify separate upstream and downstream interface lists `#9466 <https://redmine.pfsense.org/issues/9466>`__
* Prevented OpenVPN interfaces from being used by DHCP relay, since that type of interface is not compatible `#8443 <https://redmine.pfsense.org/issues/8443>`__
* Added an option to disable ping check in dhcpd `#9285 <https://redmine.pfsense.org/issues/9285>`__
* Fixed **Show all configured leases** so it is persistent after deleting a DHCP lease `#9133 <https://redmine.pfsense.org/issues/9133>`__
* Added search/filter to DHCP/DHCPv6 leases `#9791 <https://redmine.pfsense.org/issues/9791>`__
* Improved DHCP client handling of timeout conditions and script failures `#9267 <https://redmine.pfsense.org/issues/9267>`__

Diagnostics
-----------

* Fixed a PHP warning in diag_dump_states.php `#9780 <https://redmine.pfsense.org/issues/9780>`__
* Fixed reverse lookup of IPv6 addresses on diag_dns.php `#9543 <https://redmine.pfsense.org/issues/9543>`__
* Fixed diag_system_activity.php to use batch mode for top so it displays process list w/o terminal, and increased amount of output displayed `#9522 <https://redmine.pfsense.org/issues/9522>`__
* Added search/filter ARP table and NDP status `#9791 <https://redmine.pfsense.org/issues/9791>`__

DNS
---

* Added ``127.0.0.0/8`` to the DNS Resolver ``private-address`` list for DNS rebinding protection `#9708 <https://redmine.pfsense.org/issues/9708>`__
* Fixed CIDR selection issues with /32 entries in DNS Resolver Access List entries `#9586 <https://redmine.pfsense.org/issues/9586>`__
* Fixed an issue saving DNS over TLS hostnames on systems with only one gateway `#9898 <https://redmine.pfsense.org/issues/9898>`__
* Fixed an issue where manually configured DNS servers may not have been active if "allow override" was disabled and they were also assigned dynamically `#9963 <https://redmine.pfsense.org/issues/9963>`__
* Added DNS Resolver (Unbound) Python Integration `#9251 <https://redmine.pfsense.org/issues/9251>`__

Dynamic DNS
-----------

* Fixed Dynamic DNS class constructor name `#9779 <https://redmine.pfsense.org/issues/9779>`__
* Fixed errors in DNSimple Dynamic DNS `#9580 <https://redmine.pfsense.org/issues/9580>`__
* Fixed handling of wildcard (``*``) hostname entries in Cloudflare Dynamic DNS `#9361 <https://redmine.pfsense.org/issues/9361>`__
* Added support for AAAA records to Digital Ocean Dynamic DNS `#9280 <https://redmine.pfsense.org/issues/9280>`__
* Fixed issues with Digital Ocean Dynamic DNS handling of empty hostnames `#9602 <https://redmine.pfsense.org/issues/9602>`__
* Cleaned up whitespace issues in Azure Dynamic DNS backend code `#9271 <https://redmine.pfsense.org/issues/9271>`__
* Added support for Linode Dynamic DNS `#9268 <https://redmine.pfsense.org/issues/9268>`__
* Fixed issues with IPv6 on Azure Dynamic DNS `#9248 <https://redmine.pfsense.org/issues/9248>`__
* Fixed handling of wildcards in Route53 Dynamic DNS `#9053 <https://redmine.pfsense.org/issues/9053>`__
* Fixed handling of wildcards in Loopia Dynamic DNS `#8014 <https://redmine.pfsense.org/issues/8014>`__
* Fixed CloudFlare Dynamic DNS processing when ``proxied`` is enabled `#9362 <https://redmine.pfsense.org/issues/9362>`__
* Fixed CloudFlare Dynamic DNS "Invalid TTL" error due to CloudFlare API update `#10196 <https://redmine.pfsense.org/issues/10196>`__
* Changed hostname to optional for DNS-O-Matic Dynamic DNS `#7601 <https://redmine.pfsense.org/issues/7601>`__
* Added support for Gandi LiveDNS Dynamic DNS `#9452 <https://redmine.pfsense.org/issues/9452>`__

Gateways
--------

* Corrected PHP errors when marking gateways down in certain edge cases `#9851 <https://redmine.pfsense.org/issues/9851>`__

Interfaces
----------

* Added more prefix delegation size entries to selection list on interfaces.php `#9590 <https://redmine.pfsense.org/issues/9590>`__
* Added initialization to the VLAN array in console setup `#9582 <https://redmine.pfsense.org/issues/9582>`__
* Fixed issues with Netgate & hardware model detection which caused problems with default interface mappings `#8051 <https://redmine.pfsense.org/issues/8051>`__
* Fixed issues with display of previously-entered IP address values on interfaces_ppps_edit.php `#9741 <https://redmine.pfsense.org/issues/9741>`__
* Added a confirmation prompt to disconnect/release actions on status_interfaces.php `#9911 <https://redmine.pfsense.org/issues/9911>`__
* Added drivers for Mellanox ``mlx4`` and ``mlx5`` network interface cards `#7537 <https://redmine.pfsense.org/issues/7537>`__

IPsec
-----

* Fixed IPsec VTI interface creation logic `#9781 <https://redmine.pfsense.org/issues/9781>`__
* Added GUI option for IPsec P2/Child SA close action `#9767 <https://redmine.pfsense.org/issues/9767>`__
* Added IPsec DH and PFS groups 25, 26, and 27 `#9757 <https://redmine.pfsense.org/issues/9757>`__
* Added 25519 curve-based IPsec DH and PFS group 31 `#9531 <https://redmine.pfsense.org/issues/9531>`__
* Enabled NAT-T controls for IKEv2 `#9695 <https://redmine.pfsense.org/issues/9695>`__
* Improved handling of IPsec restarts breaking VTI routing `#9668 <https://redmine.pfsense.org/issues/9668>`__
* Fixed input validation that incorrectly prevented deleting IPsec P2 entries in some cases with VTI `#9258 <https://redmine.pfsense.org/issues/9258>`__
* Fixed IPsec ``keyid`` identifier handling `#9243 <https://redmine.pfsense.org/issues/9243>`__
* Fixed IPsec VTI MTU boot-time configuration `#9111 <https://redmine.pfsense.org/issues/9111>`__
* Escape Windows domain backslash in IPsec widget `#9747 <https://redmine.pfsense.org/issues/9747>`__
* Fixed VTI IPv6 address handling `#9801 <https://redmine.pfsense.org/issues/9801>`__
* Fixed Child SA button JS hide on status_ipsec.php, along with other cosmetic improvements `#8847 <https://redmine.pfsense.org/issues/8847>`__
* Added **Connect Children** button to status_ipsec.php to connect when IKE (Phase 1) is up but Child SAs (Phase 2 entries) are not `#9954 <https://redmine.pfsense.org/issues/9954>`__
* Fixed IPsec Phase 2 Remote Network field show/hide when changing between Phase 2 modes `#9720 <https://redmine.pfsense.org/issues/9720>`__
* Fixed IPsec configuration generation so that encryption options for every P2 on a given P1 are not duplicated on each P2 `#6263 <https://redmine.pfsense.org/issues/6263>`__
* Fixed a PHP error in IPsec package plugin hook processing `#10217 <https://redmine.pfsense.org/issues/10217>`__

Load Balancer
-------------

* Fixed a PHP when processing services when the configuration does not contain Load Balancer entries `#10308 <https://redmine.pfsense.org/issues/10308>`__

Logging
-------

* Moved ``igmpproxy`` logs to ``routing.log`` `#10139 <https://redmine.pfsense.org/issues/10139>`__
* Moved ``igmpproxy`` verbose logging option to ``services_igmpproxy.php`` (formerly at ``status_logs_settings.php``) `#10139 <https://redmine.pfsense.org/issues/10139>`__
* Updated ``sshguard`` and fixed a log processing regression `#9971 <https://redmine.pfsense.org/issues/9971>`__
* Fixed PHP errors in filter log processing when entries contain an invalid port `#10255 <https://redmine.pfsense.org/issues/10255>`__

Monitoring
----------

* Fixed custom view titles being forced to lower case `#9681 <https://redmine.pfsense.org/issues/9681>`__
* Fixed packet graph scaling `#9807 <https://redmine.pfsense.org/issues/9807>`__
* Fixed a PHP error in RRD processing of ALTQ data `#10248 <https://redmine.pfsense.org/issues/10248>`__

Notifications
-------------

* Fixed SMTP notification password being unintentionally changed when testing SMTP settings `#9684 <https://redmine.pfsense.org/issues/9684>`__
* Reduced frequency of GEOM rebuild notifications `#9256 <https://redmine.pfsense.org/issues/9256>`__

NTPD
----

* Added validation to ensure NTP values are treated as numbers before use `#9558 <https://redmine.pfsense.org/issues/9558>`__
* Changed the default NTP pool server to ``2.<domain>`` so that it can use IPv6 `#9931 <https://redmine.pfsense.org/issues/9931>`__
* Improved handling of errors on the NTP status page to work/fail gracefully with custom ACLs for localhost in place `#9829 <https://redmine.pfsense.org/issues/9829>`__

OpenVPN
-------

* Fixed JavaScript issue when selecting multiple OpenVPN NCP algorithms `#9756 <https://redmine.pfsense.org/issues/9756>`__
* Fixed OpenVPN wizard so it does not show DH parameter lengths that are not available `#9748 <https://redmine.pfsense.org/issues/9748>`__
* Fixed issues with OpenVPN resynchronizing when running on a gateway group `#9595 <https://redmine.pfsense.org/issues/9595>`__
* Added an option to set the OpenVPN TLS Key Direction `#9030 <https://redmine.pfsense.org/issues/9030>`__
* Added GUI options to configure OpenVPN keepalive parameters `#3473 <https://redmine.pfsense.org/issues/3473>`__
* Fixed instances of hidden invalid OpenVPN options affecting save operations `#9674 <https://redmine.pfsense.org/issues/9674>`__
* Added a copy action to OpenVPN pages `#5851 <https://redmine.pfsense.org/issues/5851>`__
* Improved sorting of bytes sent/receives on OpenVPN status page `#7359 <https://redmine.pfsense.org/issues/7359>`__
* Fixed visibility of the OpenVPN 'interface' option when multihome is selected `#7840 <https://redmine.pfsense.org/issues/7840>`__
* Reduced the OpenVPN server certificate lifetime to 398 days in the wizard to prevent errors on Apple platforms `#9825 <https://redmine.pfsense.org/issues/9825>`__
* Added input validation to prevent OpenVPN tunnel network reuse `#3244 <https://redmine.pfsense.org/issues/3244>`__
* Added Exit Notify to OpenVPN servers/client options `#9078 <https://redmine.pfsense.org/issues/9078>`__

Operating System
----------------

* Fixed serial console terminal size issues `#9569 <https://redmine.pfsense.org/issues/9569>`__
* Added the ``strings`` binary to base builds for troubleshooting `#7791 <https://redmine.pfsense.org/issues/7791>`__
* Changed UFS filesystem defaults to ``noatime`` on new installations `#9483 <https://redmine.pfsense.org/issues/9483>`__
* Fixed an issue where the IP header checksum was incorrect when reassembling packet fragments to a link with a different MTU `#10189 <https://redmine.pfsense.org/issues/10189>`__

Packet Capture
--------------

* Changed Packet Capture GUI to allow multiple TCP/UDP ports to be specified `#9766 <https://redmine.pfsense.org/issues/9766>`__
* Added start time to Packet Capture display `#9831 <https://redmine.pfsense.org/issues/9831>`__
* Added OSPF/OSPFv3 to Packet Capture protocols `#9905 <https://redmine.pfsense.org/issues/9905>`__
* Fixed Packet Capture to match both IPv4+IPv6 CARP when that protocol is selected `#9867 <https://redmine.pfsense.org/issues/9867>`__
* Fixed Packet Capture for the ``pfsync`` protocol `#10183 <https://redmine.pfsense.org/issues/10183>`__

Routing
-------

* Fixed ``(Default)`` designation on routes to match the default route in the OS `#9292 <https://redmine.pfsense.org/issues/9292>`__
* Fixed static routes remaining in routing table after removal `#9969 <https://redmine.pfsense.org/issues/9969>`__

Rules / NAT
-----------

* Fixed state kill ordering in rc.newwanip `#4674 <https://redmine.pfsense.org/issues/4674>`__
* Added the ability to search firewall logs by tracking ID `#8703 <https://redmine.pfsense.org/issues/8703>`__
* Added GUI option to disable default blocking of APIPA networks `#9966 <https://redmine.pfsense.org/issues/9966>`__
* Added more common ports to the firewall rule drop-down list `#10166 <https://redmine.pfsense.org/issues/10166>`__
* Added input validation to prevent selecting ``!*`` ("not any") in source or destination `#10168 <https://redmine.pfsense.org/issues/10168>`__
* Fixed invalid rules generated when using NAT reflection with a negated destination `#10246 <https://redmine.pfsense.org/issues/10246>`__

S.M.A.R.T.
----------

* Updated the SMART page with new capabilities `#9367 <https://redmine.pfsense.org/issues/9367>`__

SNMP
----

* Fixed SNMP sysDescr contents to include hostname and patch version `#9218 <https://redmine.pfsense.org/issues/9218>`__

Traffic Shaping / Limiters
--------------------------

* Added input validation for Limiter delay values `#9921 <https://redmine.pfsense.org/issues/9921>`__
* Fixed the queue statistics parser to handle large values `#9938 <https://redmine.pfsense.org/issues/9938>`__

Translations
------------

* Fixed an issue with international characters in configuration descriptions, which led to failures in certain cases, such as failing to set Manual Outbound NAT when the Language was set to pt_BR `#6195 <https://redmine.pfsense.org/issues/6195>`__
* Fixed a PHP error on ``system_advanced_admin.php`` when the language was set to French `#10331 <https://redmine.pfsense.org/issues/10331>`__

Upgrade / Installation
----------------------

* Revised update check to provide a more consistent version string in JSON format `#9778 <https://redmine.pfsense.org/issues/9778>`__
* Disabled serial console on VGA memstick images `#9488 <https://redmine.pfsense.org/issues/9488>`__
* Fixed a PHP error when upgrading older configurations from revision 14.4 to 14.5 `#9840 <https://redmine.pfsense.org/issues/9840>`__

UPnP
----

* Fixed display of active UPnP sessions when configured with an alternate external address `#9961 <https://redmine.pfsense.org/issues/9961>`__

User Manager / Privileges
-------------------------

* Added input validation to prevent changing the authentication server name `#9692 <https://redmine.pfsense.org/issues/9692>`__
* Added privilege to manage integrated switches `#9620 <https://redmine.pfsense.org/issues/9620>`__
* Fixed privilege matching to handle JS anchor links `#9550 <https://redmine.pfsense.org/issues/9550>`__
* Removed wildcards incorrectly used in ``isAllowedPage()`` `#9541 <https://redmine.pfsense.org/issues/9541>`__

  * This issue could prevent a user in the admins group from reaching certain pages such as the User Manager.

* Improved Deny Config Write privilege handling in the User & Group Manager `#9259 <https://redmine.pfsense.org/issues/9259>`__
* Fixed input validation of group name sizes to allow longer remote groups `#3792 <https://redmine.pfsense.org/issues/3792>`__
* Fixed handling of L2TP and PPPoE user passwords containing invalid characters `#10275 <https://redmine.pfsense.org/issues/10275>`__

Web Interface
-------------

* Corrected input validation for firewall rule VLAN priority/set `#9763 <https://redmine.pfsense.org/issues/9763>`__
* Restricted Thoth tests to arm64 in status.php NG 2569
* Added kernel memory usage to status.php output `#9705 <https://redmine.pfsense.org/issues/9705>`__
* Redacted several additional fields in status.php output `#9784 <https://redmine.pfsense.org/issues/9784>`__
  `#9729 <https://redmine.pfsense.org/issues/9729>`__
  `#9728 <https://redmine.pfsense.org/issues/9728>`__
  `#9727 <https://redmine.pfsense.org/issues/9727>`__
  `#9694 <https://redmine.pfsense.org/issues/9694>`__
  `#9736 <https://redmine.pfsense.org/issues/9736>`__
  `#9764 <https://redmine.pfsense.org/issues/9764>`__
* Fixed a potential source of PHP errors when saving per-log settings `#9540 <https://redmine.pfsense.org/issues/9540>`__
* Added GUI components for MDS mitigation `#9532 <https://redmine.pfsense.org/issues/9532>`__
* Fixed integrated switch LAGG member editing on switch_ports.php `#9447 <https://redmine.pfsense.org/issues/9447>`__
* Fixed wizard.php selection option size attribute handling `#8907 <https://redmine.pfsense.org/issues/8907>`__
* Fixed platform detection for certain C2558/C2758 systems `#6846 <https://redmine.pfsense.org/issues/6846>`__
* Set ``autocomplete=new-password`` for forms containing authentication fields to help prevent browser auto-fill from completing irrelevant fields `#9864 <https://redmine.pfsense.org/issues/9864>`__
* Fixed processing of shortcuts for XML-based packages `#9770 <https://redmine.pfsense.org/issues/9770>`__
* Updated jQuery `#9407 <https://redmine.pfsense.org/issues/9407>`__
* Improved consistency of SSL/TLS references throughout the GUI `#10172 <https://redmine.pfsense.org/issues/10172>`__
* Updated various help references and links to use the pfSense book instead of external resources `#10135 <https://redmine.pfsense.org/issues/10135>`__ `#10184 <https://redmine.pfsense.org/issues/10184>`__

XMLRPC
------

* Fixed removal of the last ALTQ traffic shaping entry from the target system when performing an XMLRPC sync `#9469 <https://redmine.pfsense.org/issues/9469>`__
* Fixed removal of the last limiter entry from the target system when performing an XMLRPC sync `#9468 <https://redmine.pfsense.org/issues/9468>`__
