# [SNMP](https://tools.ietf.org/html/rfc3411)

## Charakteristika

* **Simple Network Management Protocol** ~ jednoduchý protokol správy siete
* správa a monitorovanie zariadení pripojených v sieti a následné vyhodnocovanie prijatých dát
* súčasť sady protokolov aplikačnej vrstvy TCP/IP
* používa ho väčšina nástrojov pre správu a monitorovanie siete (Spiceworks, Solarwinds, OpenNMS, ...)

**Funkcie:**

*	schopnosť čítania/zapisovania - napr. pre vzdialené restovanie hesiel, konfigurácia IP adries
*	zbieranie informácií - reporty o chybách
*	zasielanie upozornení e-mailom (napr. o nedostatočnom mieste na disku)
*	monitorovanie CPU a pamäte servera
*	odosielanie SMS správ, ak systém padne
*	pravidelné hlásenie stavu
* iné

**SNMP sieť:**

1.	spravované zariadenia
2.	agenti
3.	spravovacie zariadenia = NMS (Network Management Station) 

<p align="center">
  <img src="https://www.manageengine.com/network-monitoring/images/snmp-components.gif" alt="SNMP Network"/>
</p>

**Princíp:**

* dopytovanie na objekty (na informácie o sieťových zariadeniach) 
* každý objekt má vlastný identifikátor, tzv. **OID** 
* OID má hierarchickú stromovú štruktúru (ako štruktúra priečinka) 
* každý z objektov v strome je očíslovaný 
* OID môže mať návratovú hodnotu rôznych typov (text, číslo, ...)



***

## Použitie

***

## Verzie

***

## Príklad


***

*Zdroje:* 

[1] https://sk.wikipedia.org/wiki/Jednoduch%C3%BD_mana%C5%BE%C3%A9rsky_protokol_siete

[2] https://cs.wikipedia.org/wiki/Simple_Network_Management_Protocol

[3] http://www.networkmanagementsoftware.com/snmp-tutorial/

[4] http://www.networkmanagementsoftware.com/snmp-tutorial-part-2-rounding-out-the-basics/

[5] https://www.manageengine.com/network-monitoring/what-is-snmp.html

[6] https://www.samuraj-cz.com/clanek/snmp-simple-network-management-protocol/

[7] https://technet.microsoft.com/en-us/library/cc783142(v=ws.10).aspx

[]

[]
