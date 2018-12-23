BGP
==================

^^^^^^^^^^^^^^^^^^^
Definition
^^^^^^^^^^^^^^^^^^^
BGP (Border Gateway Protocol) is protocol that manages how packets are routed across the internet
through the exchange of routing and reachability information between edge routers

^^^^^^^^^^^^^^^^^^^
Project description
^^^^^^^^^^^^^^^^^^^
.. image:: /_static/Images/BGP/Map.png
    :align: center

In this project, we want to ping R1 and R2 from each other using BGP.

^^^^^^^^^^^^^^^^^^^
Configuration
^^^^^^^^^^^^^^^^^^^
.. note:: Becuase configuration of the interfaces and VPCs IPs are similar to the previous projects,
          I simply just write the routing codes.

-------------------------
Routers config
-------------------------

**Border1** ::

    Border1(config)#router bgp 64520
    Border1(config-router)#network 12.12.12.0 mask 255.255.255.0
    Border1(config-router)#network 192.168.20.0
    Border1(config-router)#neighbor 12.12.12.30 remote-as 64530
    Border1(config-router)#neighbor 192.168.20.1 remote-as 64520
    Border1(config-router)#neighbor 192.168.20.1 next-hop-self

**Border2** ::

    Border2(config)#router bgp 64530
    Border2(config-router)#network 12.12.12.0 mask 255.255.255.0
    Border2(config-router)#network 192.168.30.0
    Border2(config-router)#neighbor 12.12.12.20 remote-as 64520
    Border2(config-router)#neighbor 192.168.30.2 remote-as 64530
    Border2(config-router)#neighbor 192.168.30.2 next-hop-self

**R1** ::

    R1(config)#router bgp 64520
    R1(config-router)#network 192.168.20.0
    R1(config-router)#neighbor 192.168.20.21 remote-as 64520

**R2** ::

    R2(config)#router bgp 64530
    R2(config-router)#network 192.168.30.0
    R2(config-router)#neighbor 192.168.30.32 remote-as 64530

-------------------------
View Connection details
-------------------------

Use ``sh ip route`` and ``sh ip protocol`` to see the routes and connection details.