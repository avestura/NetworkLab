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