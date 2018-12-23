Diamond IP Route
===================

^^^^^^^^^^^^^^^^^^^^
Project description
^^^^^^^^^^^^^^^^^^^^
In this section, we have four PCs and four routers in the middle. The objective is to be able to ping any PC from any other.

.. image:: /_static/Images/DiamondIPRoute/Map.png
    :align: center

^^^^^^^^^^^^^^^^^^^
Configuration
^^^^^^^^^^^^^^^^^^^

.. note:: Becuase configuration of the interfaces and VPCs IPs are like the previous project,
          I simply just write the routing codes.

**R1** ::

    R1(config)#ip route 22.22.22.0 255.255.255.0 f1/0
    R1(config)#ip route 33.33.33.0 255.255.255.0 f1/0
    R1(config)#ip route 44.44.44.0 255.255.255.0 f2/0

**R2** ::

    R2(config)#ip route 11.11.11.0 255.255.255.0 f1/0
    R2(config)#ip route 33.33.33.0 255.255.255.0 f2/0
    R2(config)#ip route 44.44.44.0 255.255.255.0 f2/0

**R3** ::

    R3(config)#ip route 11.11.11.0 255.255.255.0 f1/0
    R3(config)#ip route 22.22.22.0 255.255.255.0 f2/0
    R3(config)#ip route 44.44.44.0 255.255.255.0 f1/0

**R4** ::

    R4(config)#ip route 11.11.11.0 255.255.255.0 f2/0
    R4(config)#ip route 22.22.22.0 255.255.255.0 f2/0
    R4(config)#ip route 33.33.33.0 255.255.255.0 f1/0
