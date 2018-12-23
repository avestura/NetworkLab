EIGRP
==============

^^^^^^^^^^^^^^^^^^^
Definition
^^^^^^^^^^^^^^^^^^^
Enhanced Interior Gateway Routing Protocol (EIGRP) is an advanced distance-vector routing protocol
that is used on a computer network for automating routing decisions and configuration

^^^^^^^^^^^^^^^^^^^
Project description
^^^^^^^^^^^^^^^^^^^
.. image:: /_static/Images/EIGRP/Map.png
    :height: 500px
    :align: center

In this project, we want to ping PC5 and PC6 from each other using EIGRP *in the same area*. 

^^^^^^^^^^^^^^^^^^^
Configuration
^^^^^^^^^^^^^^^^^^^
.. note:: Becuase configuration of the interfaces and VPCs IPs are similar to the previous projects,
          I simply just write the routing codes.

-------------------------
Routers config
-------------------------

.. warning:: You should use **same area number** for routers, ping won't work otherwise!

**R1** ::

    R1(config)#router eigrp 1
    R1(config-router)#network 192.168.13.0 255.255.255.0
    R1(config-router)#network 192.168.15.0 255.255.255.0

**R2** ::

    R2(config)#router eigrp 1
    R2(config-router)#network 192.168.24.0 255.255.255.0 
    R2(config-router)#network 192.168.26.0 255.255.255.0 

**R3** ::

    R3(config)#router eigrp 1
    R3(config-router)#network 192.168.13.0 255.255.255.0 
    R3(config-router)#network 192.168.34.0 255.255.255.0 

**R4** ::

    R4(config)#router eigrp 1
    R4(config-router)#network 192.168.24.0 255.255.255.0 
    R4(config-router)#network 192.168.34.0 255.255.255.0 

-------------------------
View Connection details
-------------------------

Use ``sh ip route`` and ``sh ip protocol`` to see the routes and connection details.