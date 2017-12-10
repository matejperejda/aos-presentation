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
    <p align="center">
      <img src="https://www.manageengine.com/network-monitoring/images/snmp-get-response.gif" alt="Get request"/>
    </p>
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
     <p align="center">
      <img src="https://www.manageengine.com/network-monitoring/images/snmp-trap.gif" alt="Trap request"/>
      </p>
  * *InformRequest* (od verzie SNMPv2)
    * potvrdzovaný Trap – čaká od managera potvrdenie 
     <p align="center">
      <img src="https://www.manageengine.com/network-monitoring/images/snmp-inform-acknowledgment.gif" alt="Inform request"/>
      </p>
  *	*Response*
    * vracia väzby premenných a potvrdenie od agenta k managerovi
    *	reakcia na príkazy GetRequest, SetRequest, GetNextRequest, GetBulkRequest, InformRequest
  * *Report* (od verzie SNMPv3)
  
**SNMP datagram**
* verzia SNMP 
* autentifikačná informácia (Community String)
* typ PDU (Protocol Data Unit) – GetRequest, GetResponse, ...
* identifikátor datagramu/dotazu (pre priradenie odpovede)
* informácie o chybe 
* zoznam OID premenných a ich hodnôt 

**Verzie**
* SNMPv1
  * vznik 1988 (RFC 106, [RFC 1066](https://tools.ietf.org/html/rfc1066), [RFC 1067](https://tools.ietf.org/html/rfc1067))
  * základná funkcionalita
  * použitie pre starší HW
  * autentifikácia (spravovaného) klienta riešená pomocou „*Community String*“ (ekvivalent hesla), ktorý je prenášaný ako čistý reťazec
  * slabosť: zabezpečenie
* SNMPv2 (SNMPv2c)
  * vznik 1993
  * podporovaná najviac zariadeniami
  * odstránenie nedostatkov SNMPv1
  * nové PDU typy (*Inform*, *GetBulk*)
  * nové typy premenných (64-bitové hodnoty)
  * rozšírenie štandardnej MIB
  * pridaná kontrola doručenia (pri UDP možné straty paketov)
  * slabosť: autentifikácia stále na úrovni SNMPv1
* SNMPv3
  * vznik 2004 ([RFC 3411](http://www.ietf.org/rfc/rfc3411.txt) – [RFC 3418](http://www.ietf.org/rfc/rfc3418.txt))
  * pridané šifrovanie (zabezpečenie pomocou mena a hesla) – použitie pri prenášaní informácií cez nezabezpečené spojenia

***

## Fungovanie

SNMP je možné využívať na jednom/viac správcovských počítačoch, ktorých úlohou je sledovať/riadiť skupinu počítačov alebo iných zariadení v sieti. 

### Monitorovaná strana (spravované zariadenia)
* sieťový uzol, ktorý podporuje SNMP rozhranie
*	napr. routery, switche, VOIP telefóny, IP kamery, tlačiarne,...
*	beží na ňom proces (**agent**), zvyčajne už zabudovaný v monitorovanom zariadení, stačí ho iba aktivovať, resp. nakonfigurovať
  * slúži k správe siete na spravovanom zariadení 
  * zabezpečuje reakcie na požiadavky správcovského počítača alebo odosiela SNMP Trapy
* zhromažďujú sa informácie o stave systému (zariadenia) k následnému odosielaniu
* konfigurácia SNMP TRAP
  * agent zasiela managerovi informácie automaticky bez požiadavky
  * ak nastane vopred definovaná podmienka (napr. výpadok, kolízia), 
  * agent nečaká za odpoveďou od NMS 
* dáta agentov sú evidované ako premenné (je ich možné vzdialene modifikovať a meniť tým konfiguráciu)
* nezabezpečené SNMP
  *	prijíma požiadavky na **UDP porte 161**
  * odosiela odpovede managerovi na jeho zdrojový port
  * zasiela managerovi Trapy/Inform na **UDP porte 162**
  * agent môže generovať oznámenia z akéhokoľvek dostupného portu
*	zabezpečené SNMP (SNMPv3)
  * prijíma požiadavky na porte 10161

### Monitorovacia strana (NMS)

* spustený **monitorovací manager** 
  *	posiela požiadavky agentom na zaslanie požadovaných informácií
  *	spravuje aplikácie, ktoré monitorujú a kontrolujú spravované zariadenia
* môže existovať viac NMS v jednej spravovanej sieti
* získaný obsah sa môže ďalej rôznym spôsobom spracovávať (tabuľky, grafy, generovanie reportov, odosielanie emailov, SMS upozornení o spadnutí systému,...)
* nezabezpečené SNMP
  * posiela požiadavky k agentov z akéhokoľvek dostupného portu
  * prijíma od agenta Trapy na **UDP porte 162**
* zabezpečené SNMP (SNMPv3)
  * prijíma Trapy od agenta na porte 10162 

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
