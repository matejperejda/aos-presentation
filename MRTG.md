# [SNMP](https://tools.ietf.org/html/rfc3411)

## Charakteristika

* **Simple Network Management Protocol** ~ jednoduchý protokol spravovania siete
* správa a monitorovanie zariadení pripojených v sieti a následné vyhodnocovanie prijatých dát
* súčasť sady protokolov aplikačnej vrstvy TCP/IP
* používa ho väčšina nástrojov pre správu a monitorovanie siete (Spiceworks, Solarwinds, OpenNMS, ...)

**Funkcie**

*	schopnosť čítania/zapisovania - napr. pre vzdialené restovanie hesiel, konfigurácia IP adries
*	zbieranie informácií - reporty o chybách
*	zasielanie upozornení e-mailom (napr. o nedostatočnom mieste na disku)
*	monitorovanie CPU a pamäte servera
*	odosielanie SMS správ, ak systém padne
*	pravidelné hlásenie stavu
* iné

**SNMP sieť**

1.	spravované zariadenia
2.	agenti
3.	spravovacie zariadenia = NMS (Network Management Station) 

<p align="center">
  <img src="https://www.manageengine.com/network-monitoring/images/snmp-components.gif" alt="SNMP Network"/>
</p>

**Princíp**

* dopytovanie na "objekty" (na informácie o sieťových zariadeniach) 
* každý "objekt" má vlastný identifikátor, tzv. **OID** (Object Identifier)
* OID má hierarchickú stromovú štruktúru (ako štruktúra priečinka) 
* každý z objektov v strome je očíslovaný 
* OID môže mať návratovú hodnotu rôznych typov (text, číslo, ...)

<p align="center">
  <img src="http://25119-presscdn.pagely.netdna-cdn.com/wp-content/uploads/SNMP_OID_MIB_Tree.png" alt="OID Tree"/>
</p>

**MIB (Management Information Bases)**

* databáza OID objektov (premenných), ktoré je možné čítať, nastavovať alebo dopytovať cez SNMP
* má ju každý agent a manažér
* pomáha managerovi porozumieť SNMP odpovediam
* všetky SNMP zariadenia podporujú MIB-2, čo je štandardná sada objektov, ktoré môžu byť monitorované (napr. stav CPU, pamäť, ...)
* výrobcovia môžu dodávať vlastné MIB súbory s objektami, ktoré nie sú obsiahnuté v štandardnej sade MIB-2
* tieto upravené MIB súbory sa načítajú do NMS, aby manager vedel na ktoré SNMP objekty sa môže dopytovať
* na konkrétny objekt sa odkazuje cez cestu, ktorá pozostáva z indexov OID objektov (napr. *1.3.6.1.2.1*, to isté ako *iso.org.dod.internet.mgmt.mib-2*)

<p align="center">
  <img src="http://25119-presscdn.pagely.netdna-cdn.com/wp-content/uploads/ScreenshotOIDFolderView.png" alt="OID Tree"/>
</p>

* operácie (tzv. PDU - Protocol Data Unit): 
  * *GetRequest*
    * od managera k agentovi
    * načítanie jednej/viac premenných
    * vracia odpoveď s aktuálnymi hodnotami
  *	*GetNextRequest*
    * od managera k agentovi
    * načítanie jednej/viac premenných 
    * vracia odpoveď s hodnotou ďalšej premennej v strome, ktorá nadväzuje na predchádzajúcu premennú  (pri čítaní tabuliek)
  * *GetBulkRequest* (od verzie SNMPv2) 
    * od managera k agentovi
    * pre viac iterácií GetNextRequest
    * vracia  odpoveď s viac väzbami premenných – podstrom 
  * *SetRequest*
    * od managera k agentovi
    * pre zmenu hodnoty jednej/viac premenných
    * vracia odpoveď s novými hodnotami premenných
  * *Trap*
    * od agenta k managerovi
    * agent môže oznámiť významné udalosti pomocou nevyžiadanej správy (napr. správa o reštarte) 
  * *InformRequest* (od verzie SNMPv2)
    * potvrdzovaný Trap – čaká od managera potvrdenie 
  *	*Response*
    * vracia väzby premenných a potvrdenie od agenta k managerovi
    *	reakcia na príkazy GetRequest, SetRequest, GetNextRequest, GetBulkRequest, InformRequest
  * *Report* (od verzie SNMPv3)




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
