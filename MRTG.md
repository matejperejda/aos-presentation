# [MRTG](https://oss.oetiker.ch/mrtg/)

## Charakteristika

* **Multi Router Traffic Grapher**
* nástroj pre monitorovanie a meranie záťaže v sieti v reálnom čase
* "máme napríklad router a chceme vedieť ako je počas celého dňa vyťažený"
* monitorovanie SNMP siete a vykresľovanie grafov, ktoré ukazujú ako veľmi sú sieťové rozhrania vyťažené 
* napísaný v Perl 
* kompatibilita s Windows, Linux, Unix, Mac OS a NetWare

***

## Fungovanie

* používa [SNMP](https://github.com/matejperejda/aos-presentation/blob/master/SNMP.md) na posielanie požiadaviek s dvomi OID objektami smerom k zariadeniu
* zariadenie musí mať aktivované SNMP a k dispozícii MIB databázu pre vyhľadanie špecifikovaného OID
* zariadenie zozbiera potrebné informácie a pošle ich späť zapuzdrené v SNMP protokole
* MRTG zaznamenáva tieto údaje do logu spolu s predchádzajúcimi zaznamenanými údajmi
* z týchto záznamov vytvorí HTML dokument, ktorý obsahuje zoznam grafov s podrobnosťami o vyťaźenosti siete 

***

## Funkcie

***

## Príklad

***

*Zdroje:* 

[1] https://en.wikipedia.org/wiki/Multi_Router_Traffic_Grapher

[]

[]
