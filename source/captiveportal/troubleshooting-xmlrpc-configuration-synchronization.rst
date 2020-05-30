Troubleshooting XMLRPC Configuration Synchronization
====================================================

The following items must be checked to ensure proper XMLRPC
configuration synchronization between two nodes:

#. The **Username** and **Password** must match on all nodes
#. If not using the default admin user account, the user sync account must have the **System - HA node sync** privilege.
   No other privilege assignments are required for syncing to occur.
#. The webConfigurator must be on the same protocol on each cluster node
   (*HTTP* vs. *HTTPS*)
#. The webConfigurator must be on the same port on each cluster node
   (e.g. *443*)
#. The *Sync* interface on the secondary node must be enabled
#. The interfaces on all nodes **must be assigned in the same order**
#. The **Synchronize Config to IP** option on the primary must point to
   the sync interface IP address of the secondary
#. Traffic must be permitted to the webConfigurator port on sync
   interface of the secondary node
#. Verify that **ONLY** the primary node has the various XMLRPC config
   sync options checked

   #. Remove any IP address in the XMLRPC Sync section of the config on
      the secondary server(s)

