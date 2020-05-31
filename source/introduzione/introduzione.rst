************
Introduzione
************

Cosa significa Firew4LL?
''''''''''''''''''''''''

Da un'idea di Francesco Pellegrino di |insecurenet| e grazie all'iniziativa del 
|pin|, promosso dalla |regionepuglia|, nasce il progetto **|firew4ll|**, parola 
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

Il codice per m0n0wall era basato su FreeBSD, e |firew4ll| è un fork
di *pfSense* che è un fork di m0n0wall. 
La modifica del sistema operativo di base richiederebbe modifiche 
proibitive e potrebbe aver introdotto limitazioni da altri
sistemi operativi, richiedendo la rimozione o l'alterazione di
funzionalità.