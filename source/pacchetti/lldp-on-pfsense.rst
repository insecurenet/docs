Using LLDP on pfSense software
==============================

.. note:: Use the **LADVD** package available through the pfSense® webGUI.

lldpd
-----

`lldpd`_ allows `LLDP`_ to be enabled on pfSense software.

Install
^^^^^^^

* Navigate to **System > Packages**, **Available Packages** tab
* Search for ``lldp`` or find it in the list
* Click **Install** and **Confirm**

The package adds a menu entry under **Services > LLDP**.

Setup
^^^^^

The settings are under **Services > LLDP**, **LLDP Settings** tab.

At a minimum, check **Enable**, pick **Interfaces**, and then set other options
as desired.

Seeing neighbors
^^^^^^^^^^^^^^^^

Navigate to **Services > LLDP**, **LLDP Status** tab. The neighbors will be
printed in the lower box.

.. _lldpd: http://vincentbernat.github.io/lldpd/
.. _LLDP: https://en.wikipedia.org/wiki/Link_Layer_Discovery_Protocol
