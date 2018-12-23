Basics
==================

These are snippets and codes we use a lot in our projects

**************
Routers
**************
Codes frequently used for routers

^^^^^^^^^^^^^^
Config Mode
^^^^^^^^^^^^^^
There are multiple modes in routers, including **Normal Mode** and **Config Mode**.

You can switch to config mode with ``config terminal`` or simply ``conf t`` command and get back to normal mode with ``exit``::

    R1#
    R1# conf t
    R1(config)#
    R1(config)# exit
    R1#

.. note:: Pay attention what mode you are in.

^^^^^^^^^^^^^^
Ping
^^^^^^^^^^^^^^
You can simply ping a destination with ``ping`` command in **Normal Mode**.
If you are in **Config** mode, use ``do ping`` command.

===========================  =================================  ==================================
Mode                         Command                            Example
===========================  =================================  ==================================
Normal                       ping x.x.x.x                       ``ping 192.168.1.23``
Config                       do ping x.x.x.x                    ``do ping 192.168.1.23``
===========================  =================================  ==================================

^^^^^^^^^^^^^^^^^^^^^
Save or Show configs
^^^^^^^^^^^^^^^^^^^^^
If you are in **Normal** mode, simply type ``show running-config`` to show the current config, and
``save running-config startup-config`` to save the commands for next start.

If you are in **Config** mode, put a ``do`` prefix before those commands::

    R1# ping 192.168.1.1
    R1# show running-config
    R1# save running-config startup-config

    R1(config)# do ping 192.168.1.1
    R1(config)# do show running-config
    R1(config)# do save running-config startup-config

^^^^^^^^^^^^^^^^^
Config interfaces
^^^^^^^^^^^^^^^^^
You can config interfaces of the router in *config mode*. You may have multiple interfaces on your router such as 
**FastEthernet** or **GigabitEthernet**, etc.
Simply use ``int <interface_id>`` to config the interface. The *interface_id* parameter should be in any forms of the 
interface type, for example all of these are accepted: ``FastEthernet0/0``, ``fa0/0`` or ``f0/0``. ::

    R1#conf t
    R1(config)#int fa0/0
    R1(config-if)#ip addr 192.198.1.1 255.255.255.0
    R1(config-if)#no shut
    R1(config-if)#exit
    R1(config)#

Here we first switched to *interface config mode* with ``int fa0/0`` command and then changed
the IP address and subnet mask of the interface.
The ``shutdown`` command disables the interface. Putting a *no* (``no shutdown`` or simply ``no shut``)
before this command (re)enables the interface.

Notice that the ``exit`` command only changes the mode one level upper and does not directly switch to the *Normal mode*.

.. warning:: Interfaces of the same router can not be in the same network.
             For example you can not have two interfaces in a router with IPs ``192.168.1.1/24`` and ``192.168.1.2/24``.


^^^^^^^^^^^^^^^^^^^^^^^^
Show interface configs
^^^^^^^^^^^^^^^^^^^^^^^^
You can see the IP and status of the interfaces with ``show ip interface brief`` in Normal mode.
The shortened version ``sh ip int br`` also works. ::

    R1#show ip interface brief

    Interface                  IP-Address      OK? Method Status                Protocol
    FastEthernet0/0            192.168.1.1     YES manual up                    up
    GigabitEthernet1/0         192.168.2.1     YES manual up                    up


^^^^^^^^^^^^^^^^^^^^^^^^^^^
Add item to route table
^^^^^^^^^^^^^^^^^^^^^^^^^^^
A router must know on which interface it should to forward a packet, based on the network address of it.
You can manually add items to the routing table of a router using ``ip route x.x.x.x y.y.y.y <interface_id>`` command
where the *x.x.x.x* is the network address and *y.y.y.y* is the subnet mask. ::

    R1(config)#ip route 192.168.1.0 255.255.255.0 fa0/0

The example above simply forwards every packet with destination of ``192.168.1.x`` to its ``FastEthernet0/0`` port.

**************
VPCs
**************
Codes frequently used for VPCs

^^^^^^^^^^^^^^
Short Codes
^^^^^^^^^^^^^^
===========================  =================================  ==================================
Command                      Description                        Example
===========================  =================================  ==================================
ping x.x.x.x                 Pings an IP address                ``ping 192.168.1.23``
save                         Saves the configs of the VPC       ``save``
ip x.x.x.x/y z.z.z.z         Sets IP, Subnet mask and Gateway   ``ip 192.168.1.2/24 192.168.1.1``
ip dhcp                      Gets the IP from DHCP server       ``ip dhcp``
===========================  =================================  ==================================