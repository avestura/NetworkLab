Simple IP Route
===================

^^^^^^^^^^^^^^^^^^^^^
Project description
^^^^^^^^^^^^^^^^^^^^^

In this section, we want to ping *Microsoft* from *Google* using two routers named
*Redmond* and *California*, and vice versa.

.. image:: /_static/Images/SimpleIPRoute/AbstractMap.png
    :height: 300px
    :align: center

We just need to setup the interfaces with proper IP addresses, and then write the ip routes.
Here is a more detailed image of the project with interface identifiers and chosen example IP addresses for each interface.

.. image:: /_static/Images/SimpleIPRoute/DetailedMap.png
    :height: 300px
    :align: center

^^^^^^^^^^^^^^^
Configuration
^^^^^^^^^^^^^^^
**Microsoft VPC** ::

    Microsoft> ip 22.22.22.2/24 22.22.22.1

**Google VPC** ::

    Google> ip 11.11.11.2/24 11.11.11.1

**Redmond Router** ::


    Redmond#conf t
    Redmond(config)#int f0/0
    Redmond(config-if)#ip addr 22.22.22.1 255.255.255.0
    Redmond(config-if)#no shut
    Redmond(config-if)#exit
    Redmond(config)#int g1/0
    Redmond(config-if)#ip addr 12.12.12.2 255.255.255.0
    Redmond(config-if)#no shut
    Redmond(config-if)#exit
    Redmond(config)#ip route 11.11.11.0 255.255.255.0 g1/0


**California Router** ::

    California#conf t
    California(config)#int f0/0
    California(config-if)#ip addr 11.11.11.1 255.255.255.0
    California(config-if)#no shut
    California(config-if)#exit
    California(config)#int g1/0
    California(config-if)#ip addr 12.12.12.1 255.255.255.0
    California(config-if)#no shut
    California(config-if)#exit
    California(config)#ip route 22.22.22.0 255.255.255.0 g1/0

Now if you ping Google from Microsoft (or Microsoft from Google), this should be the result: ::

    Microsoft> ping 11.11.11.2
    84 bytes from 11.11.11.2 icmp_seq=1 ttl=62 time=69.002 ms
    84 bytes from 11.11.11.2 icmp_seq=2 ttl=62 time=37.000 ms
    84 bytes from 11.11.11.2 icmp_seq=3 ttl=62 time=45.998 ms
    84 bytes from 11.11.11.2 icmp_seq=4 ttl=62 time=39.001 ms
    84 bytes from 11.11.11.2 icmp_seq=5 ttl=62 time=31.000 ms

.. note:: Some of the first pings may timeout on your machine