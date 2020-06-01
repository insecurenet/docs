************
Introduzione
************

Cosa significa Firew4LL?
''''''''''''''''''''''''

Da un'idea di Francesco Pellegrino di |insecurenet| e grazie all'iniziativa del 
|pin|, promosso dalla |regionepuglia|, nasce il progetto |firew4ll|, parola 
formata dalle 3 parole: "Firewall", "4", "All", letteralmente **Firewall per tutti**,
che consiste nello sviluppo di un appliance con a bordo un sistema operativo, 
derivante dal fork di *pfSense*, completamente tradotto in italiano corredato da 
relativa documentazione.

Perché FreeBSD?
'''''''''''''''

Numerosi fattori sono stati presi in considerazione nella scelta del
sistema operativo di base per il progetto. Questa sezione illustra i
motivi principali per la scelta di FreeBSD.

Supporto Wireless
-----------------

Il supporto wireless è una funzionalità fondamentale per molti utenti.
Nel 2004, il supporto wireless in OpenBSD era molto limitato rispetto a
FreeBSD. OpenBSD non supportava driver o protocolli di sicurezza e non
offriva piani per la loro implementazione. Ad oggi, FreeBSD supera le
capacità wireless di OpenBSD.

Prestazioni della rete
----------------------

Le prestazioni di rete in FreeBSD sono significativamente migliori di
quelle di OpenBSD e altri os. Per distribuzioni di piccole e medie 
dimensioni, questo in genere non ha importanza, su scale superiori è 
il problema principale. 

Il supporto del multiprocessore per pf in FreeBSD consente una maggiore
scalabilità ed è utilizzato da |firew4ll|, come si attesta in questa analisi
delle prestazioni della rete:
https://github.com/gvnn3/netperf/blob/master/Documentation/netperf.pdf.

Familiarità e facilità fork
---------------------------

Il codice di *m0n0wall* era basato su FreeBSD, e |firew4ll| è un fork
di *pfSense* che è un fork di *m0n0wall*. 
La modifica del sistema operativo di base richiederebbe modifiche 
proibitive e potrebbe aver introdotto limitazioni da altri
sistemi operativi, richiedendo la rimozione o l'alterazione di
funzionalità.

Funzionalità comuni
'''''''''''''''''''

|firew4ll| è in grado di soddisfare le esigenze di quasi ogni tipo e
dimensione di ambiente di rete, da un SOHO (pmi o casa) a un data center. 
Questa sezione illustra gli scenari più comuni.

Firewall perimetrale
--------------------

La funzione più comune di |firew4ll| è quella di firewall perimetrale.
|firew4ll| supporta reti che richiedono più connessioni Internet, più reti
LAN e più reti DMZ. Sono inoltre configurabili BGP (Border Gateway
Protocol), ridondanza della connessione e capacità di bilanciamento del
carico

.. seealso:: Queste funzionalità avanzate sono descritte in *Routing* e
*Multi WAN*.

Router LAN o WAN
----------------

|firew4ll|, comunemente viene configurato come router LAN, WAN e firewall perimetrale in reti di piccole dimensioni, in reti più grandi routing LAN e WAN svolgono ruoli separati.

Router LAN
~~~~~~~~~~

|firew4ll| è una soluzione adatta per il collegamento di più segmenti
di rete interni. Questo di solito è implementato su VLAN configurate con
trunking 802.1Q.

.. note:: Viene descritto meglio nella sezione *VLAN*.

In alcuni ambienti vengono utilizzate anche interfacce Ethernet multiple. 
Gli ambienti con un alto traffico LAN con meno requisiti di filtraggio 
possono invece necessitare di switch di livello 3 o di router basati su ASIC.

Router WAN
~~~~~~~~~~

|firew4ll| è un'ottima soluzione per i provider di servizi Internet. Offre
tutte le funzionalità richieste dalla maggior parte delle reti a un
prezzo molto più basso rispetto ad altre offerte commerciali.

Apparecchi per usi speciali
---------------------------

|firew4ll| può essere utilizzato per scenari di distribuzione meno comuni
come dingolo servizio. Gli esempi includono: dispositivo VPN,
dispositivi Sniffer e dispositivo server DHCP.

Dispositivo VPN
~~~~~~~~~~~~~~~

|firew4ll| installato come un VPN server aggiunge funzionalità VPN senza 
modificare l'infrastruttura firewall esistente, includendo più protocolli VPN.

Dispositivo Sniffer
~~~~~~~~~~~~~~~~~~~

|firew4ll|offre un'interfaccia web per l'analisi di pacchetti
tcpdump. I file .cap acquisiti vengono scaricati e analizzati in
`Wireshark <http://www.wireshark.org/>`__.

.. seealso:: *Acquisizione dei pacchetti*.

Server DHCP
~~~~~~~~~~~

|firew4ll| può essere distribuito rigorosamente come un server DHCP.
Tuttavia esistono limitazioni nella GUI di |firew4ll| per la configurazione avanzata del
demone ISC DHCP.

Terminologia delle interfacce
=============================

A ogni interfaccia |firew4ll| può essere assegnato un qualsiasi nome,
ma inizialmente hanno tutti nomi predefiniti: WAN, LAN e OPT.

WAN
---

Abbreviazione di *Wide Area Network*, **WAN** è la
rete pubblica non controllata esterna firewall. In altre parole,
l'interfaccia WAN è la connessione del firewall a Internet o ad altre
reti upstream. In una distribuzione WAN multiple, WAN è la prima o
principale connessione Internet.

.. note:: Il firewall deve avere almeno un'interfaccia WAN.

LAN
---

Abbreviazione di *Local Area Network*, **LAN** è comunemente la rete privata. 
In genere utilizza uno schema di *indirizzamento IP privato* per i client locali. 
Nelle reti  di piccole dimensioni, è in genere l'unica interfaccia interna.

OPT
---

Le interfacce *OPT o opzionali* si riferiscono a qualsiasi interfaccia
aggiuntiva diversa da WAN e LAN primarie. Le interfacce OPT possono essere
segmenti LAN aggiuntivi, connessioni WAN, segmenti DMZ, interconnessioni
ad altre reti private e così via.

DMZ
---

Abbreviazione del termine militare zona demilitarizzata (*demilitarized
zone*), **DMZ** si riferisce alla zona cuscinetto tra un'area protetta e una zona di
guerra. Nella rete, è un'area in cui i server pubblici sono
raggiungibili da Internet tramite WAN, ma isolati dalla LAN. Impedisce
ai sistemi di altri segmenti di essere messi in pericolo se la rete è
compromessa, proteggendo allo stesso tempo gli host nella DMZ da altri
segmenti locali e da Internet in generale.

Denominazione dell'interfaccia di FreeBSD
-----------------------------------------

Il nome di un'interfaccia di FreeBSD inizia con il nome del suo driver
di rete. È quindi seguito da un numero che inizia da 0 e aumenta in modo
incrementale di uno per ogni interfaccia aggiuntiva che condivide quel
driver. Ad esempio, un driver comune utilizzato dalle schede di
interfaccia di rete Intel gigabit è igb. La prima di queste carte in un
sistema sarà igb0, la seconda è *igb1* e così via. Altri nomi di driver
comuni includono cxl (Chelsio 10G), em (anche Intel 1G), ix (Intel 10G),
bge (vari chipset Broadcom), tra gli altri. Se un sistema combina una
scheda Intel e una scheda Chelsio, le interfacce saranno rispettivamente
igb0 e cxl0.

.. seealso:: Le assegnazioni e la denominazione dell'interfaccia sono trattate ulteriormente in *Installazione e aggiornamento*.

Ricerca di informazioni e supporto
==================================

Tutte le richieste di informazioni e supporto possono essere trovate o trasmesse su:

 - |firew4ll|
 - |insecurenet|