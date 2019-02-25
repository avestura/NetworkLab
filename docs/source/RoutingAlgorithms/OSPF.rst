OSPF
===================

^^^^^^^^^^^^^^^^^^^
Definition
^^^^^^^^^^^^^^^^^^^
Open Shortest Path First (OSPF) is a routing protocol in form of a **graph**, operating within a single **autonomous system (AS)**
which here we call it an **Area**.

^^^^^^^^^^^^^^^^^^^
Project description
^^^^^^^^^^^^^^^^^^^
.. image:: /_static/Images/OSPF/Map.png
    :height: 500px
    :align: center

In this project, we want to ping routers from each other. There are 7 routers in 5 Areas which has different background colors
in the image.

.. warning:: Because we should set the area of the *edge routers* same as the area of destination router, here
             in this examples *area 67* and *area 14* are deleted as the area only consists of an edge router.

^^^^^^^^^^^^^^^^^^^
Configuration
^^^^^^^^^^^^^^^^^^^
.. note:: Becuase configuration of the interfaces and VPCs IPs are similar to the previous projects,
          I simply just write the routing codes.
          
.. warning:: The area number of the backbone area should be lower than others,
             it won't work otherwise. In this project it is area 0.

-------------------------
Routers config
-------------------------

**R1** ::

    R1(config)#router ospf 1
    R1(config-router)#network 12.12.12.0 255.255.255.0 area 0
    R1(config-router)#network 13.13.13.0 255.255.255.0 area 0
    R1(config-router)#network 14.14.14.0 255.255.255.0 area 0

**R2** ::

    R2(config)#router ospf 2
    R2(config-router)#network 12.12.12.0 255.255.255.0 area 0
    R2(config-router)#network 25.25.25.0 255.255.255.0 area 0
    R2(config-router)#network 26.26.26.0 255.255.255.0 area 0

**R3** ::

    R3(config)#router ospf 3
    R3(config-router)#network 13.13.13.0 255.255.255.0 area 0
    R3(config-router)#network 35.35.35.0 255.255.255.0 area 1235

**R4** ::

    R4(config)#router ospf 4
    R4(config-router)#network 14.14.14.0 255.255.255.0 area 0

**R5** ::

    R5(config)#router ospf 5
    R5(config-router)#network 25.25.25.0 255.255.255.0 area 0
    R5(config-router)#network 35.35.35.0 255.255.255.0 area 1235

**R6** ::

    R6(config)#router ospf 6
    R6(config-router)#network 26.26.26.0 255.255.255.0 area 0
    R6(config-router)#network 67.67.67.0 255.255.255.0 area 26

**R7** ::

    R7(config)#router ospf 7
    R7(config-router)#network 67.67.67.0 255.255.255.0 area 26

-------------------------
View Connection details
-------------------------

Use ``sh ip route`` and ``sh ip protocol`` to see the routes and connection details.
