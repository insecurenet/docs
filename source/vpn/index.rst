*****************************
VPN - Virtual Private Network
*****************************

.. toctree::
   :maxdepth: 2
   
   ipsec/index

.. toctree::
   :maxdepth: 2

   openvpn/index  
   
.. toctree::
   :maxdepth: 2

   l2tp/index


Scegliere una soluzione VPN
'''''''''''''''''''''''''''

Ogni soluzione VPN ha pro e contro. Questa sezione tratterà le
considerazioni principali nella scelta di una soluzione VPN, fornendo le
informazioni necessarie per scegliere quella migliore per un dato
ambiente.

Interoperabilità
================

Per interoperare con un firewall o un router prodotto da un altro
fornitore, Ipsec è di solito la scelta migliore in quanto è incluso con
quasi tutti i dispositivi con capacità VPN. Impedisce inoltre di essere
bloccato in qualsiasi particolare firewall o soluzione VPN. Per la
connettività da sito a sito interoperabile, Ipsec è di solito l'unica
scelta. OpenVPN è interoperabile con poche altre soluzioni firewall/VPN,
ma non molte. L'interoperabilità in questo senso non è applicabile ad
altri tipi di VPN poiché non sono destinati ad applicazioni sita-a-sito.

Considerazioni sull’autenticazione
==================================

Nelle versioni attuali di |firew4ll|, tutti i tipi di VPN supportano
l'autenticazione utente. Ipsec e OpenVPN possono anche funzionare con
chiavi o certificati condivisi. OpenVPN è un po' più flessibile in
questo senso perché può funzionare solo con certificati, solo con chiavi
condivise, solo con l’autenticazione dell’utente, o una combinazione di
questi. Utilizzare OpenVPN con i certificati, autenticazione TLS, e
l’autenticazione dell’utente è il metodo più sicuro. I certificati
OpenVPN possono anche essere protetti da password, nel qual caso un
certificato compromesso da solo non è adeguato per la connessione a una
VPN se è impostato per utilizzare solo i certificati. La mancanza di
autenticazione aggiuntiva può essere un rischio per la sicurezza in
quanto un sistema perso, rubato o compromesso contenente una chiave o un
certificato significa che chi ha accesso al dispositivo può connettersi
a una VPN fino a quando tale perdita viene scoperta e il certificato
revocato.

Anche se non ideale, una mancanza di username e password di
autenticazione su una VPN non è un grande rischio come può sembrare. Un
sistema compromesso può facilmente avere un logger di chiave installato
per catturare le informazioni di nome utente e password e facilmente
sconfiggere tale protezione. Nel caso di sistemi persi o rubati
contenenti chiavi, se il disco rigido non è crittografato, le chiavi
possono essere utilizzate per connettersi. Tuttavia l'aggiunta di
autenticazione password non è di grande aiuto nemmeno lì, come di solito
lo stesso nome utente e password verranno utilizzati per accedere al
computer, e la maggior parte delle password sono crackabili in pochi
minuti utilizzando l'hardware moderno quando un utente malintenzionato
ha accesso a un disco non criptato. La sicurezza delle password è spesso
compromessa dagli utenti con note sul loro laptop o nel loro case del
portatile con la password annotata. Come con qualsiasi implementazione
di sicurezza, più livelli vengono utilizzati, meglio è, ma è sempre una
buona idea mantenere questi livelli in prospettiva.

Facilità di configurazione
==========================

Nessuna delle opzioni VPN disponibili è estremamente difficile da
configurare, ma ci sono differenze tra le opzioni:

-  Ipsec ha numerose opzioni di configurazione e può essere difficile
   per i principianti.

-  OpenVPN richiede l'uso di certificati per l'accesso remoto nella
   maggior parte degli ambienti, che viene fornito con la propria curva
   di apprendimento e può essere un po' difficile da gestire. |firew4ll|
   include una procedura guidata per gestire le configurazioni di
   accesso remoto delle OpenVPN più comuni e i pacchetti di esportazione
   client delle OpenVPN facilitano il processo di attivazione dei
   client.

IPsec e OpenVPN sono opzioni preferibili in molti scenari per altri
motivi discussi in questo capitolo.

MultiWAN
========

Se gli utenti richiedono la possibilità di connettersi a più WAN, sia
IPsec che OpenVPN sono in grado di gestire tali configurazioni.

Disponibilità client
====================

Il software VPN Client è un programma che gestisce la connessione alla
VPN e la gestione di qualsiasi altra attività correlata come
l’autenticazione, la crittografia, il routing, ecc. Per le VPN di
accesso remoto, la disponibilità di software del client VPN è una
considerazione primaria. Tutte le opzioni sono compatibili con la
multipiattaforma con molti sistemi operativi diversi, ma alcuni
richiedono l'installazione di client di terze parti. IPsec in modalità
EAP-Mschapv2, IPsec in modalità EAP-TLS e IPsec in modalità Xauth sono
le uniche opzioni con supporto del client integrato in alcuni popolari
sistemi operativi desktop e mobili. Altri sistemi operativi variano e
possono includere più o meno modalità IPsec o possono anche includere
OpenVPN, come nel caso di molte distribuzioni Linux. Se l'utilizzo di
client integrati è un must, consultare la documentazione del sistema
operativo per tutte le piattaforme client richieste per vedere se è
disponibile un'opzione comune e quindi controllare |firew4ll| per vedere se
tale modalità è possibile.

In alcuni casi possono essere necessarie più VPN di accesso remoto per
ospitare tutti i client. Per esempio, IPsec potrebbe essere usato per
alcuni e OpenVPN per altri. Alcune organizzazioni preferiscono mantenere
le cose coerenti, quindi c'è un compromesso da fare, ma per motivi di
compatibilità può valere la pena offrire più opzioni.

IPsec
-----

I client Ipsec sono disponibili per Windows, Mac OS X, BSD, Linux e
altri. Anche se i client nativi possono supportare solo determinate
modalità e configurazioni specifiche. I client IPsec generici non sono
inclusi nel sistema operativo, ad eccezione di alcune distribuzioni
Linux e BSD. Una buona opzione gratuita per Windows è il client *Shrew
Soft*. Mac OS X include sia Ikev2 e Ipsec supporto di Cisco (xauth). Ci
sono opzioni gratuite e commerciali disponibili con una GUI facile da
usare per gli utenti.

OSX 10.11, insieme a Windows 7 e successivi includono il supporto per
Ipsec in modalità specifiche utilizzando Ikev2: EAP-TLS e EAP-Mschapv2.
Entrambe le opzioni sono supportate da |firew4ll| e sono coperte da
*IPsec*.

Il client Ipsec in stile Cisco incluso con i dispositivi OS X e iOS è
completamente compatibile con |firew4ll| Ipsec utilizzando xauth. La
configurazione per il client iOS è coperta dalla *configurazione del
client di IKEv2 per iOS 9*.

Molti telefoni Android includono anche un client compatibile con Ipsec,
che è discusso in *configurazione del client per IKEv2 con strongSwan
per Android*.

OpenVPN
-------

Openvpn ha client disponibili per Windows, Mac OS X, tutti i BSD, Linux,
Solaris e Windows Mobile, ma il client non viene pre-installato in
nessuno di questi sistemi operativi.

Android 4.x e i dispositivi successivi possono utilizzare un client
OpenVPN disponibile gratuitamente che funziona bene e non richiede il
rooting del dispositivo. Tale client è coperto in *Android 4.x e
versioni successive*. Versioni precedenti di Android possono anche
essere in grado di utilizzare OpenVPN tramite un client alternativo. Ci
sono altre opzioni disponibili se il dispositivo è collegato alla root,
ma questo è al di là della portata di questo libro.

iOS ha anche un client nativo OpenVPN. Per maggiori informazioni, vedere
*iOS*.

 Compatibilità con I firewall
============================-

I protocolli VPN possono causare difficoltà per molti firewall e
dispositivi NAT. Questo è principalmente rilevante per la connettività
con accesso a distanza, dove gli utenti saranno dietro una miriade di
firewall per lo più controllati da terze parti con diverse
configurazioni e funzionalità.

IPsec
-----

Ipsec utilizza sia la porta UDP 500 che il protocollo ESP per
funzionare. Alcuni firewall non gestiscono bene il traffico ESP dove è
coinvolto il NAT, perché il protocollo non ha numeri di porta come TCP e
UDP che lo rendono facilmente rintracciabile dai dispositivi NAT. I
client IPsec dietro il NAT possono richiedere il funzionamento
dell’attraversamento del NAT, che incapsula il traffico ESP sulla porta
UDP 4500.

OpenVPN
-------

OpenVPN è il più facile da usare per il firewall per le opzioni VPN.
Poiché utilizza TCP o UDP e non è influenzato da alcuna funzione NAT
comune come la riscrittura delle porte sorgente, è raro trovare un
firewall che non funzioni con OpenVPN. L'unica difficoltà possibile è se
il protocollo e la porta in uso siano bloccati. Alcuni amministratori
usano una porta comune come UDP 53 (di solito DNS), o TCP 80 (di solito
HTTP) o TCP 443 (di solito HTTPS) o per eludere la maggior parte dei
filtri in uscita.

Protezione crittografica
========================

Una delle funzioni fondamentali di una VPN è garantire la riservatezza
dei dati trasmessi.

IPsec che utilizza chiavi pre-condivise può essere rotto se viene
utilizzata una chiave debole. Utilizzare una chiave forte, almeno 10
caratteri di lunghezza con un mix di lettere, numeri e simboli maiuscoli
e minuscoli. L'uso dei certificati è preferibile, anche se un po' più
complicato da implementare.

La crittografia OpenVPN è compromessa se vengono divulgate le chiavi PKI
o condivise, anche se l'uso di fattori multipli come l'autenticazione
TLS in cima a PKI può mitigare alcuni dei pericoli.

Riepilogo
=========

La tabella *Peculiarità e caratteristiche per tipo di VPN* mostra una
panoramica delle considerazioni fornite in questa sezione.

Tabella 1: Peculiarità e caratteristiche per tipo di VPN

+==============-+=======================+================-+==========+==== ==========+================-+
| Tipo di VPN   | Client inclusi in OS  | Interoperabile  | MultiWan | Crittografia  | Facile da usare |
|               |                       |                 |          |               |                 |
+''''''''''''''=+'''''''''''''''''''''''+''''''''''''''''=+''''''''''+'''''''''''''''+''''''''''''''''=+
| IPsec         | Varia per la modalità | Si              | Si       | Si            | No (senza NAT-T)|
+==============-+=======================+================-+==========+===============+================-+
| Open-VPN      | No                    | No              | Si       | Si            | Si              |
+==============-+=======================+================-+==========+===============+================-+

Regole di firewall e VPN
''''''''''''''''''''''''

Le VPN e le regole del firewall sono gestite in modo incoerente in
|firew4ll|. Questa sezione descrive come vengono gestite le regole del
firewall per ciascuna delle singole opzioni VPN. Per le regole aggiunte
automaticamente discusse qui, l'aggiunta di tali regole può essere
disabilitata selezionando **Disabilitare tutte le regole VPN aggiunte
automaticamente** in **Sistema>Avanzate** nella scheda **Firewall/NAT**.

IPsec
=====

Il traffico IPsec che entra nell'interfaccia WAN specificata è
automaticamente permesso come descritto in IPsec. Il traffico
incapsulato all'interno di una connessione IPsec attiva è controllato
tramite regole definite dall'utente nella scheda **IPsec** in
**Firewall>Regole**.

OpenVPN
=======

OpenVPN non aggiunge automaticamente le regole alle interfacce WAN. La
procedura guidata VPN per l'accesso remoto di OpenVPN offre la
possibilità di creare opzionalmente regole per far passare il traffico
WAN e il traffico sull'interfaccia OpenVPN. Il traffico incapsulato
all'interno di una connessione OpenVPN attiva è controllato tramite
regole definite dall'utente nella scheda **OpenVPN** in
**Firewall>Regole**. Le interfacce OpenVPN possono anche essere
assegnate in modo simile ad altre interfacce su |firew4ll|. In questi casi
si applicano ancora le regole del firewall della scheda OpenVPN, ma c'è
una scheda separata specifica per l'istanza VPN assegnata che controlla
il traffico solo per quella VPN.

VPN e IPv6
''''''''''

   Ci sono alcune considerazioni speciali per le VPN quando si
   utilizzano in combinazione con Ipv6. I due punti principali di
   preoccupazione sono:

-  Se un certo tipo di VPN supporta o meno Ipv6

-  Assicurarsi che le regole del firewall non permettano traffico non
   cifrato che dovrebbe essere in arrivo su una VPN.

Supporto delle VPN a IPv6
=========================

Il supporto per Ipv6 varia da tipo a tipo e nel supporto al client.
Assicurarsi di controllare con il fornitore dell'altro dispositivo per
accertarsi che un firewall o client non-|firew4ll| supporti le VPN Ipv6.

IPsec
-----

|firew4ll| supporta l’Ipsec che utilizza Ikev1 su Ipv6 con una
particolarità: se viene utilizzato un indirizzo peer Ipv6, il tunnel può
trasportare solo reti Ipv6 in fase 2, e lo stesso per Ipv4. Il traffico
non può essere misto tra famiglie di indirizzi. *Vedere Ipsec e Ipv6*.

Quando un tunnel Ipsec è impostato per Ikev2, può includere sia le
definizioni Ipv4 che Ipv6 di fase 2 contemporaneamente.

OpenVPN
-------

Openvpn supporta pienamente Ipv6 per i client sito-a-sito e dei
dispositivi mobili e i tunnel possono trasportare sia il traffico Ipv4
che quello Ipv6 contemporaneamente. *Vedere OpenVPN e IPv6*.

VPN con IPv6 e regole del firewall
==================================

Come accennato brevemente in *Problemi con firewall e VPN*, occorre
prestare particolare attenzione quando si instrada il traffico Ipv6
attraverso una VPN e si utilizzano sottoreti pubblicamente instradabili.
Lo stesso consiglio vale anche per Ipv4, ma è molto meno comune avere
client su entrambi i lati di una VPN con Ipv4 che utilizzano indirizzi
pubblicamente instradabili.

Il problema principale è che, poiché è possibile instradare tutto da una
LAN all'altra LAN attraverso Internet, allora il traffico si potrebbe
far scorrere non cifrato tra le due reti se la VPN è down (o non è
presente affatto!). Questo è tutt'altro che ideale perché, sebbene la
connettività sia disponibile, se un traffico fosse intercettato tra le
due reti e quel traffico usasse un protocollo non criptato come HTTP,
allora potrebbe compromettere la rete.

Un modo per evitarlo è quello di non consentire il traffico dalla LAN
con IPv6 da remoto sulle regole della WAN del lato opposto. Consentire
solo il traffico dalla sottorete del lato remoto sulle regole del
firewall per qualsiasi tipo di VPN viene utilizzato per proteggere il
traffico. Una regola di blocco esplicita potrebbe anche essere aggiunta
all'inizio delle regole WAN per garantire che questo traffico non possa
entrare direttamente dalla WAN. Un metodo migliore è quello di
utilizzare una regola fluttuante per rifiutare il traffico in uscita
sulla WAN destinato ad un host delle reti locali degli host/da remoto
con VPN. In questo modo il traffico insicuro non lascia mai i locali.
Con la regola impostata per il registro, la “perdita” sarebbe ovvio per
qualcuno che monitora i registri in quanto sarebbe mostrato bloccato in
uscita sulla WAN.

Un'altra conseguenza meno ovvia di avere la connettività a doppio stack
tra le reti è che le differenze nel DNS possono causare instradamento
involontario. Supponiamo che la connettività VPN con IPv4 esista tra due
siti, ma non esista una VPN con IPv6, solo la connettività IPv6 standard
in entrambe le sedi. Se un host locale è impostato per preferire IPv6 e
riceve una risposta DNS AAAA con l'indirizzo IP con IPv6 per una risorsa
remota, tenterebbe di connettersi prima su IPv6 piuttosto che usare la
VPN. In casi come questo, sarebbe necessario fare attenzione ad
assicurarsi che il DNS non contenga record in conflitto o che le regole
fluttuanti iano aggiunte per evitare che questo traffico IPv6 fuoriusca
dalla WAN. Un articolo più approfondito su questo tipo di perdita di
traffico può essere trovato nella bozza IETF denominata
draft-gont-Opsec-vpn-leakages-00.

Le VPN forniscono un mezzo per incanalare il traffico attraverso una
connessione criptata, impedendo che venga visto o modificato durante il
transito. |firew4ll| offre tre opzioni per la VPN: IPsec, OpenVPN e L2TP.
Questo capitolo fornisce una panoramica sull'utilizzo della VPN, i pro e
i contro di ogni tipo di VPN in |firew4ll| e illustra come decidere quale
sia la soluzione migliore per un particolare ambiente. I capitoli
successivi discutono in dettaglio ogni opzione per la VPN.

L2TP è un protocollo che usa puramente il tunnel e non offre alcuna
crittografia propria. È tipicamente combinato con altri metodi di
cifratura come IPsec in modalità di trasporto. A causa di questo, non si
adatta con la maggior parte della discussione in questo capitolo. Vedere
VPN con L2TP per maggiori informazioni su L2TP.

Avviso su PPTP
''''''''''''''

Il supporto del server PPTP è stato rimosso da |firew4ll|. Nonostante
l'attrattiva della sua convenienza, PPTP non deve essere utilizzato in
nessun caso perché non è più sicuro. Questo non riguarda solo
l'implementazione di PPTP che era in |firew4ll|; qualsiasi sistema che
gestisce con PPTP non è più sicuro. Il motivo per l'insicurezza è che
PPTP si basa su MS-Chapv2 che è stato completamente compromesso. Il
traffico intercettato può essere decriptato da una terza parte al 100%
in poco tempo, quindi si può considerare qualsiasi traffico trasportato
in PPTP non cifrato. Utilizzare un altro tipo di VPN come OpenVPN o
Ipsec il più presto possibile. Ulteriori informazioni sul compromesso in
materia di sicurezza con PPTP sono disponibili all'indirizzo
https://isc.sans.edu/diary/End+of+Days+for+MS-CHAPv2/13807 e
https://www.cloudcracker.com/blog/ 2012/07/29/cracking-ms-chap-v2/.

Scenari comuni
''''''''''''''

Ci sono quattro usi comuni delle funzionalità VPN di |firew4ll|, ciascuna
trattata in questa sezione.

Connettività sito-a-sito
========================

La connettività sito-a-sito viene utilizzata principalmente per
connettere le reti in più luoghi fisici in cui è richiesta una
connessione dedicata e sempre attiva tra le sedi. Questo metodo viene
spesso utilizzato per collegare filiali a un ufficio principale,
collegare le reti di partner commerciali, o collegare una rete ad
un'altra posizione, come un ambiente di data center.

Prima della proliferazione della tecnologia VPN, i circuiti WAN privati
erano l'unica soluzione per collegare più sedi. Queste tecnologie
includono circuiti dedicati punto-a-punto, tecnologie di commutazione
dei pacchetti come frame relay e ATM, e più recentemente, MPLS
(Commutazione dell'etichetta multiprotocollo, Multiprotocol Label
Switching) e fibra e rame basato sui servizi Ethernet metropolitani.
Sebbene questi tipi di connettività WAN privata forniscano connessioni
affidabili e a bassa latenza, sono anche molto costosi con commissioni
mensili ricorrenti. La tecnologia VPN è cresciuta in popolarità perché
fornisce la stessa connettività sito-a-sito sicura utilizzando
connessioni Internet che sono generalmente molto meno costose.

Limitazioni della connettività VPN
----------------------------------

Le prestazioni sono una considerazione importante quando si pianifica
una soluzione VPN. In alcune reti, solo un circuito WAN privato può
soddisfare i requisiti di larghezza di banda o latenza. La latenza è di
solito il fattore più grande. Un circuito punto-a-punto DS1 ha una
latenza fine-a-fine di circa 3-5 ms, mentre la latenza al primo hop su
una rete ISP sarà generalmente almeno tale se non superiore. I servizi
Ethernet metropolitani o i circuiti in fibra hanno una latenza
fine-a-fine di circa 0-3 ms, solitamente inferiore alla latenza al primo
hop di una rete ISP. Qualcosa varierà in base alla distanza geografica
tra i siti. I numeri indicati sono tipici per i siti entro un paio di
centinaia di miglia l'uno dall'altro. Le VPN di solito vedono una
latenza di circa 30-60 ms a seconda delle connessioni Internet in uso e
della distanza geografica tra le posizioni. La latenza può essere
ridotta al minimo e le prestazioni della VPN massimizzate utilizzando lo
stesso ISP per tutte le sedi della VPN, ma questo non è sempre
possibile.

Alcuni protocolli funzionano molto male con la latenza inerente alle
connessioni su Internet. La condivisione di file Microsoft (SMB) è un
esempio comune. Al di sotto dei 10 ms di latenza, funziona bene. A 30 ms
o più, è lento, e a più di 50 ms è dolorosamente lento, causando
frequenti blocchi durante la navigazione delle cartelle, il salvataggio
di file, ecc. Ottenere un elenco di directory semplice richiede numerose
connessioni di andata e ritorno tra il client e il server, ciò aggrava
significativamente l'aumento del ritardo della connessione. In Windows
Vista e Server 2008, Microsoft ha introdotto SMB 2.0 che include nuove
funzionalità per affrontare il problema descritto. SMB 2.0 consente
l'invio di più azioni in una singola richiesta, così come la possibilità
di inoltrare richieste, il che significa che il client può inviare
richieste aggiuntive senza attendere la risposta da richieste
precedenti. Se una rete utilizza esclusivamente Vista e Server 2008 o
sistemi operativi più recenti questo non sarà un problema, ma data la
rarità di tali ambienti, questo dovrà di solito essere preso in
considerazione. SMB 3.0 migliora ulteriormente in questo settore con il
supporto per più flussi.

Altri due esempi di protocolli sensibili alla latenza sono il protocollo
per il desktop da remoto di Microsoft (Microsoft Remote Desktop
Protocol, RDP) e Citrix ICA. C'è una chiara differenza di prestazioni e
reattività con questi protocolli tra tempi di risposta sotto i 20 ms
tipicamente presenti in una WAN privata, e gli oltre 50-60 ms tempi di
risposta comuni alle connessioni VPN. Se gli utenti remoti lavorano su
desktop pubblicati che utilizzano dispositivi dei client leggeri, ci
sarà una notevole differenza di prestazioni tra una WAN privata e VPN.
Se tale differenza di prestazioni è abbastanza significativa da
giustificare la spesa di una WAN privata varierà da un ambiente
all'altro.

Ci possono essere altre applicazioni di rete in un ambiente sensibile
alla latenza, dove le prestazioni ridotte di una VPN sono inaccettabili.
O tutte le posizioni possono essere all'interno di un'area geografica
relativamente piccola utilizzando lo stesso ISP, dove le prestazioni di
una VPN rivaleggiano con quelle di connessioni WAN private.

Accesso remoto
==============

Le VPN con accesso da remoto consentono agli utenti di connettersi in
modo sicuro a una rete da qualsiasi luogo in cui sia disponibile una
connessione Internet. Questo è più frequentemente utilizzato per i
lavoratori da dispositivi mobili (spesso indicato come “Combattenti di
strada o Road Warriors”) o perché il lavoro richiede frequenti viaggi e
poco tempo in ufficio, o per dare ai dipendenti la possibilità di
lavorare da casa. Può anche consentire agli appaltatori o ai fornitori
l'accesso temporaneo a una rete. Con la proliferazione degli smartphone,
gli utenti hanno la necessità di accedere in modo sicuro ai servizi
interni dai loro telefoni utilizzando una VPN con accesso da remoto.

Protezione delle reti wireless 
==============================

Una VPN può fornire un ulteriore livello di protezione per le reti
wireless. Questa protezione è duplice: fornisce un ulteriore livello di
crittografia per il traffico che attraversa la rete wireless e può
essere implementata in modo tale da richiedere un'ulteriore
autenticazione prima di consentire l'accesso alle risorse di rete.
Questo è distribuito per lo più come VPN con accesso da remoto. Questo è
coperto in *Protezione aggiuntiva per una rete wireless*.

Relay sicuro
============

Le VPN con accesso da remoto possono essere configurate in modo da
passare tutto il traffico dal sistema client attraverso la VPN. Questo è
conveniente da avere quando si utilizzano reti non attendibili, come
hotspot wireless in quanto consente ad un client di spingere tutto il
suo traffico Internet attraverso la VPN e verso Internet dal server VPN.
Questo protegge l'utente da una serie di attacchi che sono possibili su
reti non attendibili, anche se ha un impatto sulle prestazioni in quanto
aggiunge ulteriori salti e latenza a tutte le connessioni. Tale impatto
è di solito minimo con connettività ad alta velocità quando il client e
il server VPN sono relativamente vicini geograficamente.
