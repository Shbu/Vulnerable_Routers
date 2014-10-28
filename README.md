Vulnerable-Routers
==================

Vulnerable routers by different manufacturers that doesn't have any fix till date for a lurking backdoor.


Summary:
--------------------------
Cisco has disclosed the existence of an undocumented backdoor in several of their routers offerings which could a remote attacker to “gain root-level access to an affected device” by way of an unknown test interface in the TCP service listening on port 32764

Confidentiality:
--------------------------
On many devices this undocumented interface can only be accessed from the local or wireless network, but on some devices it is also accessible from the Internet. There could be potential instances where attackers can gain access to these devices from internet and gather information for personal benefits.

Integrity:
------------------------
It is stated that an attacker could exploit this vulnerability by accessing the affected device from the LAN-side interface and issuing arbitrary commands in the underlying operating system. An exploit could allow the attacker to access user credentials for the administrator account of the device, manipulate them at his will and read the device configuration. It can also allow attacker to issue arbitrary commands on the device with escalated privileges.

Availability:
---------------------------
Currently there is no report that this swath of devices that have this backdoor issue are attacked from outsiders. As attacker can issue commands from remote locations, once accessed, he can manipulate the device and effect it’s availability at his will through internet.


Resolution:
----------------------
1.	Cisco said that currently there are no workarounds that would mitigate the vulnerabilities, but they are planning to release software updates to mitigate them. The significant downside to this announcement is that these devices will remain unpatched for the foreseeable future till the updates are in position.
2.	At most, wireless users should be aware of such attacks and be vigilant in upgrading their antivirus and device firmware as soon as upgrades are released.


More information:
------------------------------------------------------
More information on official CISCO website:
http://tools.cisco.com/security/center/content/CiscoSecurityAdvisory/cisco-sa-20140110-sbd 

Article on CISCO Routers:
---------------------------------
http://www.cio.com/article/745860/Cisco_Promises_to_Fix_Admin_Backdoor_in_Some_Routers?source=rss_security&utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%3A+cio%2Ffeed%2Fdrilldowntopic%2F3089+%28CIO.com+-+Security%29&utm_content=Netvibes 
 
Some random code/data about the backdoor we found in inksys WAG200G (TCP/32764).

The backdoor may be present in other hardware, We'll update this readme accordingly.

Possible fix :
-------------------------------
If it's listening on the internet: add a firewall rule in the web UI (@domainzero)
It also seems to work on the LAN side. (issue 35)
but apparently, not for every body (issue 57) so use the PoC again after adding the rule to make sure the firewall does its job.
Install an open source firmware (for example OpenWRT or Tomato) this is NOT magical, OpenWAG200 is vuln: http://sourceforge.net/projects/openwag200/files/OpenWAG200/1.4/
kill the backdoor after each reboot (issue 61 & TCP-32764-First-Aid)
use this alternative firmware: amod (thank you pidocchio and nremond)
redirect the port traffic in your router firewall to a local unused IP and done ([@osisecurite])

Probable source of the backdoor:
--------------------------------------------
SerComm https://news.ycombinator.com/item?id=6998258 (nice finding :) )
Confirmed by a header (socket_header.h) in cisco gpl sources (thank you Andreas Fett!)

Backdoor LISTENING ON THE INTERNET confirmed in :
------------------------------------------------
 * Linksys WAG120N (@p_w999)
 *	Netgear DG834B V5.01.14 (@domainzero)
 *	Netgear DGN2000 1.1.1, 1.1.11.0, 1.3.10.0, 1.3.11.0, 1.3.12.0 (issue 44)
 *	Netgear WPNT834 (issue 79)
 *	OpenWAG200 maybe a little bit TOO open ;) (issue 49)


Backdoor confirmed in:
------------------------------------
 •	Cisco RVS4000 fwv 2.0.3.2 & 1.3.0.5 (issue 57)
 •	Cisco WAP4410N (issue 11)
 •	Cisco WRVS4400N
 •	Cisco WRVS4400N (issue 36)
 •	Diamond DSL642WLG / SerComm IP806Gx v2 TI (https://news.ycombinator.com/item?id=6998682)
 •	LevelOne WBR3460B (http://www.securityfocus.com/archive/101/507219/30/0/threaded)
 •	Linksys RVS4000 Firmware V1.3.3.5 (issue 55)
 •	Linksys WAG120N (issue 58)
 •	Linksys WAG160n v1 and v2 (@xxchinasaurxx @saltspork)
 •	Linksys WAG200G
 •	Linksys WAG320N (http://zaufanatrzeciastrona.pl/post/smieszna-tylna-furtka-w-ruterach-linksysa-i-prawdopodobnie-netgeara/)
•	Linksys WAG54G2 (@_xistence)
•	Linksys WAG54GS (@henkka7)
•	Linksys WRT350N v2 fw 2.00.19 (issue 39)
•	Linksys WRT300N fw 2.00.17 (issue 34)
•	Netgear DG834[∅, GB, N, PN, GT] version < 5 (issue 19 & issue 25 & issue 62 & jd & Burn2 Dev)
•	Netgear DGN1000 (don't know if there is a difference with the others N150 ones... issue 27)
•	Netgear DGN1000[B] N150 (issue 3)
•	Netgear DGN2000B (issue 26)
•	Netgear DGN3500 (issue 13)
•	Netgear DGND3300 (issue 56)
•	Netgear DGND3300Bv2 fwv 2.1.00.53_1.00.53GR (issue 59)
•	Netgear DM111Pv2 (@eguaj)
•	Netgear JNR3210 (issue 37)

Backdoor may be present in:
------------------------------------
•	All SerComm manufactured devices (https://news.ycombinator.com/item?id=6998258)
•	Linksys WAG160N (http://zaufanatrzeciastrona.pl/post/smieszna-tylna-furtka-w-ruterach-linksysa-i-prawdopodobnie-netgeara/)
•	Netgear DG934 probability: probability: 99.99% (http://codeinsecurity.wordpress.com/category/reverse-engineering/)
•	Netgear WG602, WGR614 (v3 doesn't work, maybe others...) (http://zaufanatrzeciastrona.pl/post/smieszna-tylna-furtka-w-ruterach-linksysa-i-prawdopodobnie-netgeara/)


Backdoor is not working in:
---------------------------------------
•	Belkin F5D7230-4 6000 (SerComm manufactured product) (issue 51)
•	Belkin F9K1002 v3 (SerComm manufactured product)
•	Cisco E2000 fwv 1.0.02 (issue 17)
•	Cisco Linksys E4200 V1 fwv 1.0.05 (issue 18)
•	Cisco Linksys X2000 (issue 40)
•	Cisco EPC3925
•	Cisco RV082 v03 fw4.2.2.08 (issue 94)
•	Linksys E2500 (@Antoniojojojo)
•	Linksys E3000 fwv 1.0.04 (issue 16)
•	Linksys E3200 Firmware Version: 1.0.04 (Build 1)
•	Linksys E4200 Firmware Version: 2.0.26 (issue 53)
•	Linksys RV082 v02 fw2.0.2.01-tm (issue 94)
•	Linksys WAG354G V.2 EU (issue 69)
•	Linksys WRT100 fwv 1.0.00 (Issue 71)
•	Linksys WRT110 fwv 1.0.07 (issue 70)
•	Linksys WRT120N fwv 1.0.07 (@viniciuskmax)
•	Linksys WRT160Nv2 (issue 43)
•	Linksys WRT320N (issue 31)
•	Linksys WRT54GL(v1.1) Firmware v4.30.16
•	Linksys WRT54GS v1.52.8 build 001 (thanks Helmut Tessarek)
•	Linksys WRT600N running 1.01.36 build 3 (@shanetheclassic & issue 46)
•	Linksys WRT610N V1 fwv 1.00.03 B15 (issue 60)
•	Netgear CG3100 (issue 6)
•	Netgear CG3700EMR as provided by ComHem Sweden (issue 20)
•	Netgear DG834G v5 (manufactured by Foxconn as opposed to the previous versions, nice finding anthologist issue 28)
•	Netgear DGN2200Bv3 (V1.1.00.23_1.00.23) (issue 41)
•	Netgear DGN3500 (amod 9.3.1 based on official 1.1.00.34 - http://alfie.altervista.org/amod)
•	Netgear DGND3700 (issue 33)
•	Netgear DGND4000 (V1.1.00.14_1.00.14) (issue 67)
•	Netgear ProSafe FVS318G fwv 3.1.1-14 (thank you Jason Leake :) )
•	Netgear R4500 firmware V1.0.0.4_1.0.3 (issue 64)
•	Netgear R6300 (issue 15)
•	Netgear R7000 (@LRFLEW)
•	Netgear RP614v[4,2] V1.0.8_02.02 (issue 22 & issue 24)
•	Netgear VMDG480 (aka. VirginMedia SuperHub) swv 2.38.01 (issue 16)
•	Netgear VMDG485 (aka. VirginMedia SuperHub 2) swv1.01.26 (issue 16)
•	Netgear WGR614v3 (issue 8)
•	Netgear WGR614v7 (thanks "Martin from germany" [your e-mail doesn't work])
•	Netgear WGR614v9 (issue 7)
•	Netgear WN2500RP (issue 15)
•	Netgear WNDR3700 (@juliengrenier)
•	Netgear WNDR4000 (issue 10)
•	Netgear WNDR4500 (@TechnicalRah)
•	Netgear WNR2000v3 (issue 43)
•	Netgear WNR3500L firmware V1.2.2.30_34.0.37 (issue 65)
•	Netgear WNR3500Lv2
•	Sercomm AD81ABA



Source: An additional listing of vulnerable devices has been compiled and placed in below link by a developer:
https://github.com/elvanderb/TCP-32764
