.. _acme-validation-methods:

Validation Methods
------------------

Let's Encrypt can validate by checking the contents of a TXT record in DNS, or
by fetching a file in a known location from a web server running on the hostname
it is validating.

.. _acme-validation-nsupdate:

nsupdate
^^^^^^^^

The ``nsupdate`` method uses RFC2136 style DNS updates to populate a TXT record
in DNS to validate ownership of the domain.

We recommend using this method as it does not require external inbound access,
so it can be used for internal systems that do not allow or cannot receive
Internet traffic.

Before starting, an appropriate DNS key and settings must be in place in the DNS
infrastructure for the domain to allow the host to update a TXT DNS record for
``_acme-challenge.<domain name>``.

To use this method:

* Add an entry to the **Domain SAN list**
* **Mode**: Enabled
* Enter domain name (e.g. ``myhost.example.com``)
* Set **Method** to *DNS-NSupdate / RFC 2136*
* Click + to expand the method-specific settings
* Fill in the info

  :Server: The IP address or hostname of the DNS server to which the updates are
    sent.
  :Key Name: The name of the update key. Leave blank unless it is different than
    ``_acme-challenge.<domain name>``.
  :Key Algorithm: The algorithm used for the key
  :Key: The update key for this record

* Ensure the other options are set properly, per :ref:`acme-create-certificate`.
* Click **Save**
* Click **Issue/Renew**

.. _acme-validation-dns-manual:

DNS-Manual
^^^^^^^^^^

The manual DNS method can be utilized when a firewall cannot receive inbound
traffic and it does not have access to any automatic DNS-based method.

The **manual** in the name indicates that the process **must be performed by
hand** both initially and when it is time to renew the certificate. The firewall
obtains the authorization value and then the TXT record must be manually created
or updated with this value.

We do not recommend using this method unless no other method is available.

To use this method:

* Add an entry to the **Domain SAN list**
* **Mode**: Enabled
* Enter domain name (e.g. ``myhost.example.com``)
* Set **Method** to *DNS-Manual*
* Click **Save**
* Click **Issue**
* Locate the record info in the output::

    [Mon Feb 6 14:49:23 EST 2017] Add the following TXT record:
    [Mon Feb 6 14:49:23 EST 2017] Domain: '_acme-challenge.www.example.com'
    [Mon Feb 6 14:49:23 EST 2017] TXT value: 'xPrykHSri5epT5yrJJWyY536Z1T51r_Ef4LkWJry-iw'
    [Mon Feb 6 14:49:23 EST 2017] Please be aware that you prepend _acme-challenge. before your domain
    [Mon Feb 6 14:49:23 EST 2017] so the resulting subdomain will be: _acme-challenge.www.example.com
    [Mon Feb 6 14:49:23 EST 2017] Please add the TXT records to the domains, and retry again.

* Add or update the TXT record in the domain's DNS server for
  ``_acme-challenge.<domain name>`` with the TXT value from the output
* Wait approximately 2 minutes, or longer, for DNS to propagate
* Click **Renew**

.. _acme-validation-dns-namecheap:

Namecheap API
^^^^^^^^^^^^^

For certain accounts with Namecheap, API access may be obtained that allows
remote manipulation of DNS records. This can be used with the ACME package to
validate certificates for domains with DNS hosted at Namecheap using their
BasicDNS servers. This requires ACME package version 0.5.1 or later.

.. warning:: The Namecheap DNS API requires that the client read all records and
   then write them all back when making any change. This is potentially
   dangerous. Take a backup of all DNS records on the domain before attempting
   to use the API.

The first step is to request API access:

* Login to a Namecheap account
* Navigate to **Profile > Tools** under the account
* Look for **Namecheap API Access** under **Business & Dev Tools**
* If the status does not say **On**, then click **Manage** and change the slider to **On**.

  .. note:: API access must be approved by Namecheap. There are qualifications
     to meet, such as a specific number of domains or a balance on the account.
     Check the Namecheap API documentation for more information. The process is
     documented as taking 2 days, but may take longer. If API access is not
     enabled after several days, contact Namecheap support.

Once the API is enabled, then perform the following steps:

* Login to a Namecheap account
* Navigate to **Profile > Tools** under the account
* Look for **Namecheap API Access** under **Business & Dev Tools**
* Click **Manage**
* Note the API key for use in the ACME package
* Click **Edit** and add whitelisted IP addresses that can contact the API using
  this API key.

Now setup the account in the ACME package:

* Add an entry to the **Domain SAN list**
* **Mode**: Enabled
* Enter domain name (e.g. ``myhost.example.com``)
* Set **Method** to *DNS-Namecheap*
* Click + to expand the method-specific settings
* Fill in the info

  :API Key: The API Key displayed in the Namecheap API Access manager, as
    described previously.
  :Username: The Namecheap account username associated with the API Key.

* Ensure the other options are set properly, per :ref:`acme-create-certificate`.
* Click **Save**
* Click **Issue/Renew**

.. _acme-validation-dns-other:

Other DNS Methods
^^^^^^^^^^^^^^^^^

The package contains several additional DNS-based methods for other providers.
These work similar to the nsupdate method above, but have configuration values
specific to each provider. Contact the DNS provider or server administrator to
obtain the necessary settings or credentials.

.. _acme-validation-ftp:

FTP Webroot
^^^^^^^^^^^

The **FTP webroot** method is useful when the firewall is performing NAT (port
forward or 1:1) or reverse proxy duty for handling traffic for the domain. The
firewall can use SFTP or FTPS to store the domain validation files on a web
server behind the firewall so it does not have to host the files itself.

We recommend using this method when no DNS update method is available for use by
the firewall.

To use this method:

* Add an entry to the **Domain SAN list**
* **Mode**: Enabled
* Enter domain name (e.g. ``myhost.example.com``)
* Set **Method** to *webroot FTP*
* Click + to expand the method-specific settings
* Fill in the required info:

  :Server: The server where the package will send the challenge response files,
    e.g. ``sftp://x.x.x.x``

    .. note:: This method supports supports ``sftp://`` and ``ftps://`` servers.

  :Username/password: Credentials for the SFTP/FTPS account
  :Folder: *Full path* to the target directory including
    ``/.well-known/acme-challenge`` at the end

    .. warning:: Make sure the specified user has write permissions to the
       directory!

* Click **Save**
* Click **Issue/Renew**

.. _acme-validation-localfolder:

Webroot Local Folder
^^^^^^^^^^^^^^^^^^^^

This method works similar to FTP Webroot but with the files hosted on the
firewall itself. This method cannot be utilized by the WebGUI web server as that
would mean exposing the GUI to the Internet, which is a major security issue.

This method can, however, be used in conjunction with the HAProxy package to
host the files on the firewall itself in some circumstances. See
https://forum.netgate.com/post/677786 for details.

.. _acme-validation-standalone:

Standalone
^^^^^^^^^^

The **Standalone** method runs a small web server natively that is active only
while the validation process is running.

.. warning:: This service **must** be accessible using port 80 for security
   reasons!

If the firewall is using port 80 for another service, such as the WebGUI, then
this method may not be viable. If the service on the port is public, then it
cannot be used. If the service is private, then it may be possible to relocate
the existing service or bind the update method to an alternate port, then port
forward on the WAN interface. The standalone binding should only be changed if
the port is forwarded via NAT to a different port (e.g. 80 forwarded to 8080)

A firewall rule must allow traffic to the target port at all times, it cannot be
automatically enabled and disabled in the current package. If port 80 is used by
the standalone service, the WebGUI redirect must be disabled on **System >
Advanced** using the **Disable webConfigurator redirect rule** option. If the
redirect is active when standalone mode attempts to use the port, it will print
an error message stating that ``socat`` is unable to bind to the port.

.. warning:: We do not recommend using this method as it exposes a service on
   the firewall to the Internet. Only use this method if no other method is
   available.

To use this method:

* Add an entry to the **Domain SAN list**
* **Mode**: Enabled
* Enter domain name (e.g. ``myhost.example.com``)
* Set **Method** to *standalone HTTP server*
* Click + to expand the method-specific settings
* Fill in the port number when using a non-default port
* If the domain name for the firewall has both an A and AAAA DNS record, check
  **Bind to IPv6 instead of IPv4** so that validation can occur over IPv6.
* Click **Save**
* Click **Issue/Renew**
