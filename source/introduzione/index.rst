************
Introduzione
************

Cosa significa Firew4LL?
''''''''''''''''''''''''

Da un'idea di Francesco Pellegrino di |insecurenet| e grazie all'iniziativa del 
|pin|, promosso dalla |regionepuglia|, nasce il progetto ** |firew4ll| **, parola 
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

|firew4ll| configurato come router LAN o WAN e firewall perimetrale è una
distribuzione comune in reti di piccole dimensioni. Il routing LAN e WAN
svolgono ruoli separati in reti più grandi.

Router LAN
~~~~~~~~~~

|firew4ll| è una soluzione adatta per il collegamento di più segmenti
di rete interni. E' più comunemente distribuito con VLAN configurate con
trunking 802.1Q.

.. note:: Viene descritto meglio nella sezione *VLAN*.

Anche interfacce Ethernet multiple sono utilizzate in alcuni ambienti.
Gli ambienti con alto traffico LAN e requisiti di filtro
potrebbero richiedere invece switch di livello 3 o router basati su
ASIC.

Router WAN
~~~~~~~~~~

pfSense è un'ottima soluzione per i provider di servizi Internet. Offre
tutte le funzionalità richieste dalla maggior parte delle reti a un
prezzo molto più basso rispetto ad altre offerte commerciali.

Apparecchi per usi speciali
---------------------------

pfSense può essere utilizzato per scenari di distribuzione meno comuni
come dispositivo autonomo. Gli esempi includono: dispositivo VPN,
dispositivo Sniffer e dispositivo server DHCP.

Dispositivo VPN
~~~~~~~~~~~~~~~

Il software pfSense installato come un'appliance di rete privata
virtuale separata aggiunge funzionalità VPN senza interrompere
l'infrastruttura firewall esistente e include più protocolli VPN.

Dispositivo Sniffer
~~~~~~~~~~~~~~~~~~~

pfSense offre un'interfaccia web per l'analizzatore di pacchetti
tcpdump. I file .cap acquisiti vengono scaricati e analizzati in
`Wireshark <http://www.wireshark.org/>`__.

Vedere anche:
~~~~~~~~~~~~~

Per ulteriori informazioni sull'uso delle funzionalità di acquisizione
dei pacchetti di pfSense, consultare: *Acquisizione dei pacchetti*.

Appliance del server DHCP
~~~~~~~~~~~~~~~~~~~~~~~~~

pfSense può essere distribuito rigorosamente come un server del
Protocollo di configurazione dell’host dinamico, tuttavia esistono
limitazioni della GUI di pfSense per la configurazione avanzata del
daemon DHCP ISC.

Vedere anche:
~~~~~~~~~~~~~

Per ulteriori informazioni sulla configurazione del servizio DHCP su
pfSense, consulta *IPv4 DHCP Server DHCP dell’IPv4* e *Annunci del
server DHCP e router IPv6*


