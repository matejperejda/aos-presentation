# [MRTG](https://oss.oetiker.ch/mrtg/)

- [Charakteristika](#charakteristika)
- [Fungovanie](#fungovanie)
- [Funkcie](#funkcie)
- [Návod](#návod)

## Charakteristika

* **Multi Router Traffic Grapher**
* nástroj pre monitorovanie a meranie záťaže sieťových rozhraní v reálnom čase 
* "máme napríklad router a chceme vedieť ako je počas celého dňa vyťažený"
* monitorovanie SNMP siete a vykresľovanie grafov, ktoré ukazujú ako veľmi sú sieťové rozhrania vyťažené 
* napísaný v Perl 
* kompatibilita s Windows, Linux, Unix, Mac OS a NetWare

<p align="center">
  <img src="https://www.pcwdld.com/wp-content/uploads/gui-screenshot.jpg" alt="MRTG example"/>
</p>

***

## Fungovanie

* využíva [SNMP](https://github.com/matejperejda/aos-presentation/blob/master/SNMP.md) protokol na posielanie požiadaviek s dvomi OID objektami smerom k zariadeniu
* zariadenie musí mať aktivované SNMP a k dispozícii MIB databázu pre vyhľadanie špecifikovaných OID objektov
* zariadenie zozbiera potrebné informácie a pošle ich späť zapuzdrené v SNMP protokole
* MRTG zaznamenáva tieto údaje do logu spolu s predchádzajúcimi zaznamenanými údajmi
* z týchto záznamov vytvorí HTML dokument, ktorý obsahuje zoznam grafov s podrobnosťami o vyťaźenosti každého dostupného sieťového rozhrania 

***

## Funkcie

* meranie dvoch hodnôt (I – input, O – output) v rámci jedného sledovaného sieťového rozhrania
*	získanie dát prostredníctvom SNMP agenta alebo cez pomocou príkazového riadoka (spustenia skriptu `mrtg`)
* predvolene zhromažďuje údaje každých päť minút (možnosť nastaviť inak)
* generuje HTML stránku pre každé sledované zariadenie, ktorá obsahuje štyri grafy (reálny ćas, 7 dní, 5 týždňov, 12 mesiacov)
* výsledky sú vykresľované na časovej osi (I – zelená plná oblasť, O – modrá krivka)
* vyznačuje maximálne, priemerné a aktuálne hodnoty pre I a O
* môže odosielať výstražné emaily, ak je prekročená nejaká hraničná hodnota 
* monitorovanie rôznych vlastností systému (otáčky ventilátora CPU, informácie o prihlásení do systému,...)

***

## Návod

### Windows - [link](https://oss.oetiker.ch/mrtg/doc/mrtg-nt-guide.en.html)

**Prerekvizity**
* [Perl](https://www.activestate.com/activeperl/downloads)
  * prítomnosť skontrolovať v CMD pomocou `perl -v`
* [MRTG](https://oss.oetiker.ch/mrtg/pub/?M=D)
  * stiahnuť zip a extrahovať súbory
* Aktivovať SNMP service 
  * Ovládací panel - Programy a súčasti - Zapnúť alebo vypnúť súčasti systému Windows - SNMP - OK
  * Start - services.msc - SNMP Service
    * Traps - Community name: "public", Trap destination: "127.0.0.1" 
    * Security - Accepted comunity names: "public, READ ONLY", Accept SNMP packets from these hosts: "localhost"

**Konfigurácia MRTG**

```bash
cd ..\mrtg-2.17.4\bin
perl cfgmaker public@localhost --global --output server.cfg
```
> `public` - READ ONLY community string

> `localhost` - IP adresa zariadenia

> `mrtg.cfg` - meno výsledného konfiguračného súboru

**Nastavenie cesty k reportom**
* Ukladanie reportov do špeciálneho adresára
  * v `server.cfg` doplniť cestu k reportom `WorkDir: ..\mrtg-2.17.4\reports`
* Pravidelné volanie MRTG 
  * do `server.cfg` doplniť `RunAsDaemon: yes`

**Spustenie MRTG**

`perl mrtg server.cfg`


***

*Zdroje:* 

[1] https://en.wikipedia.org/wiki/Multi_Router_Traffic_Grapher

[2] https://linux.die.net/man/1/mrtg

[]
