# [MRTG](https://oss.oetiker.ch/mrtg/)

- [Charakteristika](#charakteristika)
- [Fungovanie](#fungovanie)
- [Funkcie](#funkcie)
- [Príklad](#príklad)

## Charakteristika

* **Multi Router Traffic Grapher**
* nástroj pre monitorovanie a meranie záťaže v sieti v reálnom čase
* "máme napríklad router a chceme vedieť ako je počas celého dňa vyťažený"
* monitorovanie SNMP siete a vykresľovanie grafov, ktoré ukazujú ako veľmi sú sieťové rozhrania vyťažené 
* napísaný v Perl 
* kompatibilita s Windows, Linux, Unix, Mac OS a NetWare

***

## Fungovanie

* využíva [SNMP](https://github.com/matejperejda/aos-presentation/blob/master/SNMP.md) protokol na posielanie požiadaviek s dvomi OID objektami smerom k zariadeniu
* zariadenie musí mať aktivované SNMP a k dispozícii MIB databázu pre vyhľadanie špecifikovaných OID objektov
* zariadenie zozbiera potrebné informácie a pošle ich späť zapuzdrené v SNMP protokole
* MRTG zaznamenáva tieto údaje do logu spolu s predchádzajúcimi zaznamenanými údajmi
* z týchto záznamov vytvorí HTML dokument, ktorý obsahuje zoznam grafov s podrobnosťami o vyťaźenosti siete 

***

## Funkcie

* meranie dvoch hodnôt (I – input, O – output) v rámci jedného sledovaného zariadenia
*	získanie dát prostredníctvom SNMP agenta alebo cez pomocou príkazového riadoka (spustenia skriptu `mrtg`)
* predvolene zhromažďuje údaje každých päť minút (možnosť nastaviť inak)
* generuje HTML stránku pre každé sledované zariadenie, ktorá obsahuje štyri grafy (reálny ćas, 7 dní, 5 týždňov, 12 mesiacov)
* výsledky sú vykresľované na časovej osi (I – zelená plná oblasť, O – modrá krivka)
* vyznačuje maximálne, priemerné a aktuálne hodnoty pre I a O
* môže odosielať výstražné emaily, ak je prekročená nejaká hraničná hodnota 
* monitorovanie rôznych vlastností systému (otáčky ventilátora CPU, informácie o prihlásení do systému,...)

***

## Príklad

***

*Zdroje:* 

[1] https://en.wikipedia.org/wiki/Multi_Router_Traffic_Grapher

[2] https://linux.die.net/man/1/mrtg

[]
