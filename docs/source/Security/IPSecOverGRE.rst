IPSec over GRE
=================

^^^^^^^^^^^^^^^^^^^
Definition
^^^^^^^^^^^^^^^^^^^
Generic Routing Encapsulation (GRE) is a tunneling protocol that can encapsulate a wide variety of network layer protocols
inside virtual point-to-point links or point-to-multipoint links over an Internet Protocol network.

Internet Protocol Security (IPsec) is a secure network protocol suite that authenticates and encrypts the packets of data sent over an internet protocol network. It is used in virtual private networks (VPNs).

^^^^^^^^^^^^^^^^^^^
Project description
^^^^^^^^^^^^^^^^^^^
.. image:: /_static/Images/IPSec/IPSEC.png
    :align: center

Here in the image, the green tunnel is the GRE tunnel which is secured by IPSEC protocol.
We want to secure the packets that 'Aryan' and 'Hasti' PCs are sending to eachother.

^^^^^^^^^^^^^^^^^^^
Configuration
^^^^^^^^^^^^^^^^^^^
.. note:: You can use any routing algorithm you learnt in previous sections for the four router in the middle (called Internet).
          In this section, I ignore the four routers and assume that they are preconfigured.

-------------------------
Routers config
-------------------------

.. note:: You can change the the key part(``hastiaryan``) and the profile name part(``OurProfile``) to your custom names.

**Astaneh** ::

    Astaneh(config)#crypto isakmp policy 10
    Astaneh(config-isakmp)#authentication pre-share
    Astaneh(config-isakmp)#exit    
    Astaneh(config)#crypto isakmp key hastiaryan address 4.4.4.101
    Astaneh(config)#crypto ipsec transform-set 3des-sha esp-3des esp-sha-hmac
    
    Astaneh(config)#crypto ipsec profile OurProfile
    Astaneh(ipsec-profile)#set transform-set 3des-sha
    Astaneh(ipsec-profile)#exit

    Astaneh(config)#interface Tunnel0
    Astaneh(config-if)#ip address 172.16.1.1 255.255.255.0
    Astaneh(config-if)#tunnel source FastEthernet0/0
    Astaneh(config-if)#tunnel destination 4.4.4.101
    Astaneh(config-if)#tunnel protection ipsec profile OurProfile
    Astaneh(config-if)#exit

    Astaneh(config)#ip route 192.168.4.0 255.255.255.0 Tunnel0

**Tehran** ::

    Tehran(config)#crypto isakmp policy 10
    Tehran(config-isakmp)#authentication pre-share
    Tehran(config-isakmp)#exit    
    Tehran(config)#crypto isakmp key hastiaryan address 1.1.1.101
    Tehran(config)#crypto ipsec transform-set 3des-sha esp-3des esp-sha-hmac
    
    Tehran(config)#crypto ipsec profile OurProfile
    Tehran(ipsec-profile)#set transform-set 3des-sha
    Tehran(ipsec-profile)#exit

    Tehran(config)#interface Tunnel0
    Tehran(config-if)#ip address 172.16.1.4 255.255.255.0
    Tehran(config-if)#tunnel source FastEthernet0/0
    Tehran(config-if)#tunnel destination 1.1.1.101
    Tehran(config-if)#tunnel protection ipsec profile OurProfile
    Tehran(config-if)#exit

    Tehran(config)#ip route 192.168.1.0 255.255.255.0 Tunnel0
