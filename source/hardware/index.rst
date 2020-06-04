********
Hardware
********

Requisiti minimi hardware
'''''''''''''''''''''''''

I requisiti minimi per |firew4ll| 0.1-RELEASE-p3 sono:

-  CPU 600 MHz o più veloce
-  RAM 512 MB o più
-  Unità disco da 4 GB o superiore (SSD, HDD, ecc.)
-  Una o più schede di interfaccia di rete compatibili
-  Unità USB di avvio o CD/DVD-ROM per l'installazione iniziale

.. note:: I requisiti minimi non sono adatti a tutti gli ambienti; vedere la *Guida al dimensionamento dell'hardware* per i dettagli

Selezione dell’Hardware
'''''''''''''''''''''''

L'uso di sistemi operativi open source con hardware non testato può creare conflitti hardware/software. *Ottimizzazione hardware e
risoluzione dei problemi* offre suggerimenti per la risoluzione di vari problemi.

Previeni mal di testa per la scelta dell’hardware
=================================================

Usare l'hardware ufficiale di |firew4ll|
----------------------------------------

Consigliamo vivamente di utilizzare l’hardware ufficiale dal |firew4ll|
Store. Il nostro hardware è stato sviluppato per assicurare alla
comunità che piattaforme hardware specifiche sono state testate e
validate a fondo.


Convenzioni dei nomi
--------------------

In tutta la guida ci riferiamo all'architettura hardware a 64 bit
come "amd64", la designazione dell'architettura usata da FreeBSD. Intel
ha adottato l'architettura creata da AMD per x86-64, quindi il nome
amd64 si riferisce a tutte le CPU x86 a 64 bit.


Guida alle dimensioni dell’hardware
===================================

Durante il dimensionamento dell'hardware per |firew4ll|, la velocità
effettiva richiesta e le funzionalità necessarie sono i fattori primari
che influenzano la selezione dell'hardware.

Considerazioni sulla velocità effettiva
---------------------------------------

I requisiti minimi sono sufficienti se sono richiesti meno di 100 Mbps
di throughput non crittografato. Per requisiti di throughput più
elevati, seguire queste linee guida basate su estese esperienze di test
e implementazione.

L'hardware a cui fa riferimento questa sezione è disponibile nel *|firew4ll|
Store.* Le specifiche generali dell'hardware sono disponibili nella
tabella *Hardware |firew4ll|*.


Nelle reti reali il flusso del traffico conterrà probabilmente pacchetti
di dimensioni variabili, non tutte così grandi, ma dipende dall'ambiente
e dal tipo di traffico coinvolto. La tabella *500.000 PPS di throughput
in varie dimensioni di frame* elenca alcune dimensioni di pacchetti
comuni e il throughput ottenuto con una velocità di 500.000 pacchetti al
secondo.

Tabella 1: 500.000 PPS di throughput in varie dimensioni di frame

+--------------+--------------------------+
| Frame size   | Throughput at 500 Kpps   |
+==============+==========================+
| 64 bytes     | 244 Mbps                 |
+--------------+--------------------------+
| 500 bytes    | 1.87 Gbps                |
+--------------+--------------------------+
| 1000 bytes   | 3.73 Gbps                |
+--------------+--------------------------+
| 1500 bytes   | 5.59 Gbps                |
+--------------+--------------------------+

Differenza di prestazioni per tipo di scheda di rete
----------------------------------------------------

La scelta della scheda NIC ha un impatto significativo sulle
prestazioni. Le schede economiche e di fascia bassa consumano molta più
CPU rispetto alle schede di migliore qualità come Intel. Il primo
scoglio per il throughput del firewall è throughput migliora in modo
significativo utilizzando una scheda NIC di qualità migliore con CPU più
lente. Al contrario, aumentando la velocità della CPU non aumenterà
proporzionalmente il throughput se abbinato a una scheda di rete di
bassa qualità.

Considerazioni sulle funzioni
=============================

Funzionalità, servizi e pacchetti abilitati sul firewall possono ridurre
il throughput potenziale totale in quanto consumano risorse hardware che
potrebbero altrimenti essere utilizzate per trasferire il traffico di
rete. Ciò è particolarmente vero per i pacchetti che intercettano o
ispezionano il traffico di rete, come Snort o Suricata.

La maggior parte delle funzionalità del sistema di base non tiene conto
in modo significativo del dimensionamento dell'hardware, ma alcune
possono potenzialmente avere un impatto notevole sull'utilizzo
dell'hardware.

Tabelle di stato
----------------

Le connessioni di rete attive attraverso il firewall sono tracciate
nella tabella di stato del firewall. Ogni connessione attraverso il
firewall consuma due stati: uno che entra nel firewall e uno che esce
dal firewall. Ad esempio, se un firewall deve gestire 100.000
connessioni client simultanee del server Web, la tabella di stato deve
essere in grado di contenere 200.000 stati.

I firewall in ambienti che richiedono un numero elevato di stati
simultanei devono disporre di RAM sufficiente per contenere la tabella
degli stati. Ogni stato richiede circa 1 KB di RAM, il che rende il
calcolo dei requisiti di memoria relativamente facile. La tabella
*Consumo RAM di una tabella di stato grande* fornisce una guida per la
quantità di memoria richiesta per dimensioni di tabelle stato più
grandi. Questa è esclusivamente la memoria utilizzata per il rilevamento
dello stato. Il sistema operativo stesso insieme ad altri servizi
richiederà almeno 175-256 MB di RAM aggiuntiva e possibilmente di più a
seconda delle funzionalità utilizzate.

Tabella 2: Consumo RAM di una tabella di stato ampia

+-------------+---------------+-----------------+
| Stati       | Connessioni   | RAM Richiesta   |
+=============+===============+=================+
| 100,000     | 50,000        | ~97 MB          |
+-------------+---------------+-----------------+
| 500,000     | 250,000       | ~488 MB         |
+-------------+---------------+-----------------+
| 1,000,000   | 500,000       | ~976 MB         |
+-------------+---------------+-----------------+
| 3,000,000   | 1,500,000     | ~2900 MB        |
+-------------+---------------+-----------------+
| 8,000,000   | 4,000,000     | ~7800 MB        |
+-------------+---------------+-----------------+

È più sicuro sopravvalutare i requisiti. Sulla base delle informazioni
di cui sopra, una buona stima sarebbe che 100.000 stati consumerebbero
circa 100 MB di RAM o che 1.000.000 stati consumerebbero circa 1 GB di
RAM.

VPN (tutti i tipi)
------------------

La domanda che i clienti pongono in genere sulle VPN è "Quante
connessioni può gestire il mio hardware?" Questo è un fattore secondario
nella maggior parte delle distribuzioni ed è di minore importanza.
Quella metrica è un effetto di come altri fornitori hanno concesso in
licenza funzionalità VPN in passato e non ha un equivalente diretto
specifico in |firew4ll|. La considerazione principale nel dimensionamento
hardware per VPN è il potenziale throughput del traffico VPN.

La crittografia e la decrittografia del traffico di rete con tutti i
tipi di VPN richiede molta CPU. |firew4ll| offre diverse opzioni di
cifratura da utilizzare con IPsec. Le varie cifre funzionano in modo
diverso e il throughput massimo di un firewall dipende dalla cifra
utilizzata e dalla possibilità o meno che tale cifra possa essere
accelerata dall'hardware.

Gli acceleratori di crittografia hardware aumentano notevolmente la
velocità effettiva massima della VPN ed eliminano in gran parte la
differenza di prestazioni tra le cifre accelerate. La tabella *Velocità
effettiva VPN per modello hardware, tutti i valori sono in Mbit/s*
illustra la velocità effettiva massima per i vari componenti hardware
disponibili nell'archivio |firew4ll| quando si utilizza IPsec e OpenVPN.

Per IPsec, AES-GCM è accelerato da AES-NI ed è più veloce non solo per
questo, ma anche perché non richiede un algoritmo di autenticazione
separato. IPsec ha anche un overhead di elaborazione del sistema
operativo per pacchetto inferiore rispetto a OpenVPN, quindi per ora
IPsec sarà quasi sempre più veloce di OpenVPN.

Tabella 3: Velocità effettiva VPN per modello hardware, tutti i valori
sono in Mbit/s

+------------+--------------------------+-------------------------+
|  Modello   | OpenVPN/AES-128+SHA1     | IPsec/IKEv2+AES-GCM     |
+============+==========================+=========================+
|            | TCP 1400B                | TCP 1400B               |
+------------+--------------------------+-------------------------+
|Firew4ll-ISN| 103                      | 98                      |
+------------+--------------------------+-------------------------+

Laddove un throughput VPN elevato è un requisito per un firewall,
l'accelerazione crittografica dell'hardware è della massima importanza
per assicurare non solo velocità di trasmissione elevate, ma anche
ridurre il sovraccarico della CPU. La riduzione del sovraccarico della
CPU significa che non ridurrà le prestazioni di altri servizi sul
firewall. L'attuale migliore accelerazione è disponibile utilizzando una
CPU che include il supporto AES-NI combinato con AES-GCM in IPsec.

Pacchetti
---------

Alcuni pacchetti hanno un impatto significativo sui requisiti hardware e
il loro uso deve essere preso in considerazione quando si seleziona
l'hardware.

Snort/Suricata
--------------

Snort e Suricata sono pacchetti |firew4ll| per il rilevamento delle
intrusioni nella rete. A seconda della loro configurazione, possono
richiedere una quantità significativa di RAM. 1 GB deve essere
considerato come minimo, ma alcune configurazioni potrebbero richiedere
almeno 2 GB.

Suricata è multi-thread e può potenzialmente sfruttare NETMAP per IPS
inline se l'hardware offre supporto.

Squid
-----

Squid è un server proxy HTTP con memorizzazione nella cache disponibile
come pacchetto |firew4ll|. Le prestazioni di I/O del disco sono una
considerazione importante per gli utenti di Squid poiché determinano le
prestazioni della cache. Al contrario, la velocità del disco è in gran
parte irrilevante per la maggior parte dei firewall |firew4ll| poiché
l'unica attività significativa del disco è il tempo di avvio e il tempo
di aggiornamento; non ha rilevanza per la velocità di trasmissione della
rete o altre normali operazioni.

Anche per Squid qualsiasi disco rigido sarà sufficiente in piccoli
ambienti. Per oltre 200 implementazioni utente, un SSD di alta qualità
di un OEM di livello 1 è un must. Un SSD di bassa qualità potrebbe non
essere in grado di sopportare le numerose scritture legate al
mantenimento dei dati memorizzati nella cache.

Le dimensioni della cache di squid incidono anche sulla quantità di RAM
richiesta per il firewall. Squid consuma circa 14 MB di RAM per 1 GB di
cache su amd64. A quel ritmo, una cache da 100 GB richiederebbe 1,4 GB
di RAM per la sola gestione della cache, senza contare le altre esigenze
di RAM per squid.

Ottimizzazione dell'hardware e risoluzione dei problemi
'''''''''''''''''''''''''''''''''''''''''''''''''''''''

l sistema operativo che sostiene |firew4ll| può essere messo a punto in
molti modi. Alcuni di questi parametri sintonizzabili sono disponibili
in |firew4ll| in **Opzioni avanzate** (Vedere scheda *Sintonizzabili di
sistema*). Altri sono indicati nell'\ *ottimizzazione* della pagina
principale di FreeBSD (7).

L'installazione predefinita del software |firew4ll| include un set completo
di valori ottimizzati per una buona prestazione senza essere
eccessivamente aggressivo. Ci sono casi in cui hardware o driver
richiedono la modifica di valori o un carico di lavoro di rete specifico
richiede modifiche per funzionare in modo ottimale. L'hardware venduto
nel *negozio |firew4ll|* è ulteriormente ottimizzato poiché abbiamo una
conoscenza dettagliata dell'hardware, che elimina la necessità di fare
affidamento su ipotesi più generali.

Modifiche comuni lungo queste linee per altro hardware sono disponibili
nella pagina wiki della *documentazione per la sintonizzazione e la
risoluzione dei problemi delle schede di rete.*

.. note:: Le modifiche a /boot/loader.conf.local richiedono il riavviodel firewall.

Eusarimento del Mbuf
====================

Un problema comune riscontrato dagli utenti dei commmodity hardware è
l'esaurimento di mbuf. Per i dettagli su mbufs e il monitoraggio
dell'utilizzo di mbuf, consultare *Cluster Mbuf*. Se il firewall
esaurisce mbufs, può causare il panico del kernel e il riavvio con
determinati carichi di rete che esauriscono tutti i buffer di memoria di
rete disponibili. Ciò è più comune con le schede di rete che utilizzano
più code o che sono altrimenti ottimizzate per le prestazioni rispetto
all'utilizzo delle risorse. Inoltre, l'utilizzo di mbuf aumenta quando
il firewall utilizza determinate funzionalità come *Limiters* Per
aumentare la quantità di mbuf disponibili, aggiungere quanto segue a
``/boot/loader.conf.local``::
  kern.ipc.nmbclusters="1000000"

Inoltre, le schede potrebbero aver bisogno di altri valori simili
aumentati come kern.ipc.nmbjumbop. Oltre ai grafici sopra menzionati,
controlla l'output del comando netstat -m per verificare se ci sono aree
vicine all'esaurimento.

NIC Queue Count Conteggio code NIC
==================================

Per motivi di prestazioni, alcuni tipi di schede di rete utilizzano più
code per l'elaborazione dei pacchetti. Su sistemi multi-core, in genere
un driver vorrà utilizzare una coda per core della CPU. Esistono alcuni
casi in cui ciò può portare a problemi di stabilità, che possono essere
risolti riducendo il numero di code utilizzate dalla scheda di rete. Per
ridurre il numero di code, specificare il nuovo valore in
``/boot/loader.conf.local``, come ad esempio::
  hw.igb.num_queues=1

Il nome dell'OID sysctl varia in base alla scheda di rete, ma di solito
si trova nell'output di sysctl -a, sotto hw. <drivername>.

Disabilitare MSIX
=================

Un altro problema comune è una scheda di rete che non supporta
correttamente MSIX nonostante le sue affermazioni. MSIX può essere
disabilitato aggiungendo la seguente riga in */boot/loader.conf.local*::
  hw.pci.enable_msix=0

La distribuzione del software |firew4ll| è compatibile con la maggior parte
di hardware supportati da FreeBSD.

|firew4ll| è compatibile con l'hardware di
architettura a 64 bit (amd64, x86-64).

Compatibilità Hardware
''''''''''''''''''''''

Il modo migliore per garantire che l'hardware sia compatibile con il software |firew4ll| è acquistare hardware dallo store |firew4ll| poichè sono stati testati e noti per funzionare bene con |firew4ll|. L'hardware nello store viene testato con ogni versione del software |firew4ll| ed è ottimizzato per le prestazioni.

Per le soluzioni casalinghe, le note hardware di FreeBSD sono la migliore risorsa per determinare la compatibilità hardware. |firew4ll| versione 01-RELEASE-p3 si basa su 11.2-RELEASE-p14, quindi l'hardware compatibile si trova nelle note hardware sul sito Web di FreeBSD.
Un'altra buona risorsa è la sezione Hardware delle FAQ di FreeBSD.

Adattatori di rete
==================

Una vasta gamma di schede Ethernet cablate (NIC) sono supportate da
FreeBSD e sono quindi compatibili con i firewall |firew4ll|. Tuttavia, non
tutte le schede di rete sono uguali. L'hardware può variare notevolmente
in termini di qualità da un produttore all'altro.

Raccomandiamo le schede NIC Intel PRO/1000 1Gb e PRO/10GbE 10Gb
perché hanno un solido supporto per i driver in FreeBSD e funzionano
molto bene. La maggior parte dell'hardware venduto nel negozio |firew4ll|
contiene schede di rete Intel.

Delle varie altre schede PCIe/PCI supportate da FreeBSD, alcune
funzionano bene. Altre potrebbero avere problemi come le VLAN che non
funzionano correttamente, non essere in grado di impostare velocità o
duplex o avere prestazioni scadenti. In alcuni casi, FreeBSD può
supportare una particolare scheda di rete ma, con implementazioni
specifiche del chipset, il supporto del driver o può essere scadente. In
caso di dubbi, cerca nel forum |firew4ll| le esperienze di altri utenti che
utilizzano lo stesso hardware o simile.

Quando un firewall richiede l'uso di VLAN, selezionare adattatori che
supportano l'elaborazione VLAN nell'hardware. Questo è discusso in *LAN
virtuali (VLAN).*

Adattatori di rete USB
----------------------

Si sconsiglia di utilizzare adattatori di rete USB di qualsiasi marca /
modello a causa della loro inaffidabilità e scarse prestazioni.

Adattatori wireless
-------------------

Gli adattatori e i dispositivi wireless supportati sono trattati in *Wireless*.
