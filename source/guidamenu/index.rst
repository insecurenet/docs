*************
Guida ai menu
*************

Sistema
'''''''

Il menu del **Sistema** contiene opzioni per il firewall stesso, opzioni
generali e avanzate, aggiornamenti, pacchetti aggiuntivi, utenti e
routing.

    **Avanzate** Impostazioni avanzate per firewall, hardware, SSH,
    notifiche, parametri sintonizzabili e molti altri. Vedere *Opzioni
    di configurazione avanzate*.

    **Gestione dei certificati** Gestire le autorità di certificazione,
    i certificati e gli elenchi di revoche di certificati (x.509).
    Vedere *Gestione dei certificati*.

    **Impostazioni generali** Impostazioni generali come nome host,
    dominio e server DNS. Vedere *Opzioni della configurazione
    generale*.

    **Sync con elevata disponibilità** Controlla il modo in cui i nodi
    |firew4ll| in un cluster ad alta disponibilità (HA) sincronizzano gli
    stati e la configurazione. Vedere *Elevata disponibilità*.

    **Disconnettersi** Esce dalla GUI, riportando l'utente alla
    schermata di accesso. Vedere *Gestione utenti e Autenticazione*.

    **Gestione di pacchetti** Componenti aggiuntivi dei software
    aggiuntivi per |firew4ll| per espandere la sua funzionalità. Vedere
    *Pacchi*.

    **Routing** Gestisce gateway, route statiche e gruppi gateway per
    multi-WAN. Vedere *Routing*.

    **Procedura guidata di configurazione** La procedura guidata di
    configurazione esegue la configurazione iniziale di base. Vedere
    ***Installazione guidata***.

    **Aggiornare** Aggiorna |firew4ll| all'ultima versione. Vedere
    *Aggiornamento tramite WebGUI*.

    **Gestione utenti** Gestire utenti, gruppi e server di
    autenticazione (RADIUS o LDAP) per l'accesso alla GUI, l'accesso
    VPN, ecc. Vedere *Gestione e autenticazione dell'utente*.

	.. note::
		Se un utente dispone del privilegio *WebCfg - Sistema: Gestione della password dell’utente*, questa opzione di menu porta l'utente a una pagina in cui è possibile modificare la propria password ma non apportare modifiche ad altri utenti.

    **Impostazioni utente** Se le impostazioni per utente sono
    abilitate, questa pagina consente agli utenti di ignorare le opzioni
    di comportamento predefinite disponibili in **Impostazione
    generale**.

Interfacce
''''''''''

Il menu **Interfacce** contiene una voce per l'assegnazione delle
interfacce e voci per ciascuna interfaccia attualmente assegnata. Le
interfacce assegnate mostreranno i loro nomi configurati o i nomi
standard se non sono stati modificati (ad es. WAN, LAN, OPTx)

    **(assegnare)** Assegna interfacce a ruoli logici (ad es. WAN, LAN,
    OPT) e creare/mantenere VLAN e altri tipi di interfacce virtuali.
    Vedere *Configurazione dell'interfaccia*, *Tipi di interfaccia e
    configurazione*, e *LAN virtuali (VLAN)*.

    **WAN** Configura l'interfaccia WAN. Vedere *Configurazione
    dell'interfaccia*.

    **LAN** Configura l'interfaccia LAN. Vedere *Configurazione
    dell'interfaccia*.

    **OPTX** Configura eventuali interfacce opzionali aggiuntive. Vedere
    *Configurazione dell'interfaccia*.

Firewall
''''''''

Le voci del menu **Firewall** configurano le regole del firewall, le
regole NAT e la loro struttura di supporto.

    **Alias** Gestisce raccolte di indirizzi IP, reti o porte per
    semplificare la creazione e la gestione delle regole. Vedere
    *alias*.

    **NAT** Gestisce le regole NAT che controllano le porte forward, NAT
    1:1 e il comportamento NAT in uscita. Vedere *Traduzione
    dell'indirizzo di rete*.

    **Regole** Configura le regole del firewall. C'è una scheda su
    questa schermata per ogni interfaccia configurata, oltre a schede
    per gruppi e diversi tipi di VPN, quando abilitati. Vedere
    *Introduzione alla schermata delle regole del firewall*.

    **Pianificazioni** Gestisce le pianificazioni delle regole basate
    sul tempo. Vedere *Regole basate sul tempo*.

    **Shaper del traffico** Gestisce le impostazioni di shaping del
    traffico/Qualità di servizio (QoS). Vedere *Shaper del traffico*.

    **IP virtuali** Configura gli indirizzi IP virtuali che consentono a
    |firew4ll| di gestire il traffico per più di un indirizzo IP per
    interfaccia, in genere per le regole NAT o la disponibilità elevata.
    Vedere *Indirizzi IP virtuali*.

Servizi
'''''''

Il menu **Servizi** contiene elementi che controllano i servizi forniti
dai daemon in esecuzione sul firewall. Vedere *Servizi*.

    **captive portal** Controlla il servizio Cadel captive portal che
    indirizza gli utenti a una pagina Web per l'autenticazione prima di
    consentire l'accesso a Internet. Vedere *captive portal*.

    **Relay DHCP** Configura il servizio di relay di DHCP che inoltra le
    richieste DHCP da un segmento di rete a un altro. Vedere *Relay DHCP
    e DHCPv6*.

    **Server DHCP** Configura il servizio DHCP che fornisce la
    configurazione automatica dell'indirizzo IP per i client. Vedere
    *Server DHCP IPv4*.

    **Relay DHCPv6** Configura il servizio di inoltro DHCP per IPv6 che
    inoltra richieste DHCPv6 da un segmento di rete a un altro. Vedere
    *Relay DHCP e DHCPv6*.

    **Server DHCPv6 e RA** Configura il servizio DHCP per IPv6 e gli
    annunci router che forniscono la configurazione automatica
    dell'indirizzo IPv6 per i client. Vedere *Server DHCP IPv6 e annunci
    del router.*

    **Forwarder del DNS** Configura il forwarder del DNS di cache
    incorporato. Vedere *Forwarder del DNS*.

    **Risolutore del DNS** Configura il risolutore DNS di cache
    incorporato. Vedere *Risolutore del DNS*.

    **DNS dinamico** Configura i servizi DNS dinamici ("dyndns") che
    aggiorna un server dei nomi remoto quando l'indirizzo IP della WAN
    di questo firewall è cambiato. Vedere *DNS dinamico*.

    **Proxy IGMP** Configura il proxy del protocollo di gestione del
    gruppo interno per il passaggio del traffico multicast tra le
    interfacce. Vedere *Proxy IGMP*.

    **Bilanciatore del carico** Configura il bilanciatore del carico,
    che bilancia le connessioni in entrata su più server locali. Vedere
    *Bilanciamento del carico del server*.

    **NTP** Configura il demone del server del protocollo dell’orario di
    rete. Vedere *NTPD*.

    **Server PPPoE** Configura il server PPPoE che accetta e autentica
    le connessioni dai client PPPoE su reti locali. Vedere *Server
    PPPoE*.

    **SNMP** Configura il demone SNMP (Protocollo di gestione della rete
    semplice, Simple Network Management Protocol) per consentire la
    raccolta di statistiche basate sulla rete da questo firewall. Vedere
    *SNMP*.

    **UPnP e NAT-PMP** Configura il servizio Universal Plug and Play
    (UPnP) e il protocollo di mappatura delle porte del NAT che
    configura automaticamente le regole NAT e firewall per i dispositivi
    che supportano gli standard UPnP o NAT-PMP. Questa voce di menu
    appare solo se è assegnata più di un'interfaccia. Vedere *UPnP e
    NAT-PMP*.

    **Attivare la LAN** Configura le voci Attivare la LAN che attivano
    in remoto i dispositivi dei client locali. Vedere *Attivare la LAN*.

VPN
'''

Il menu VPN contiene elementi relativi alle reti private virtuali (VPN),
tra cui IPsec, OpenVPN e L2TP. Vedere *Reti private virtuali*.

    **IPsec** Configura tunnel VPN di IPsec, IPsec mobile e impostazioni
    IPsec. Vedere *IPsec*.

    **L2TP** Configura i servizi e gli utenti L2TP. Vedere *VPN con
    L2TP*.

    **OpenVPN** Configura server e client OpenVPN, nonché la
    configurazione specifica del client. Vedere *OpenVPN*.

Stato
'''''

Le voci del menu **Stato** mostrano informazioni sullo stato e registri
per vari componenti e servizi del sistema.

    **captive portal** Quando il captive portal è abilitato, questa
    voce mostra lo stato dell'utente e del voucher. Vedere *Portale
    captive*.

    **CARP (failover)** Mostra lo stato degli indirizzi IP del CARP su
    questo firewall, come lo stato MASTER/BACKUP per ciascun VIP del
    CARP. Ha anche controlli per la modalità di manutenzione HA. Vedere
    *Controllare lo stato CARP*.

    **Pannello di controllo** Un collegamento alla pagina principale del
    firewall |firew4ll|, che visualizza informazioni generali sul sistema.
    Vedere *Pannello di controllo*.

    **Locazioni di DHCP** Mostra un elenco di tutte le locazioni di DHCP
    IPv4 assegnate da questo firewall e fornisce controlli basati su
    tali leasing, come l'aggiunta di mappature statiche. Vedere
    *Locazioni*.

    **Leasing DHCPv6** Mostra un elenco di tutti i lease DHCP IPv6
    assegnati da questo firewall. Vedere *Locazioni*

    **Ricaricare filtro** Mostra lo stato dell'ultima richiesta di
    ricarica del filtro, comprese le azioni di ricarica attive. Fornisce
    inoltre un mezzo per forzare un ricaricamento del filtro e per
    forzare una sincronizzazione della configurazione XMLRPC quando è
    configurato HA. Vedere *Risoluzione dei problemi relativi alle
    regole del firewall*.

    **Gateway** Mostra lo stato dei gateway e dei gruppi gateway per
    multi-WAN. Vedere *Routing*.

    **Interfacce** Mostra lo stato hardware per le interfacce di rete,
    equivalente all'utilizzo di ifconfig sulla console. Vedere *Stato
    dell'interfaccia*.

    **IPsec** Mostra lo stato di tutti i tunnel IPsec configurati.
    Vedere *IPsec*.

    **Bilanciamento del carico** Mostra lo stato dei pool di
    bilanciamento del carico del server. Vedere\ *Visualizzazione dello
    stato del bilanciamento del carico*.

    **Monitoraggio** Mostra i dati rappresentati graficamente per le
    statistiche di sistema come larghezza di banda utilizzata, utilizzo
    della CPU, stati del firewall, ecc. Vedere *Grafici di
    monitoraggio*.

    **NTP** Mostra lo stato del daemon del server del protocollo
    dell’orario di rete. Vedere *NTPD*.

    **OpenVPN** Mostra lo stato di tutte le istanze OpenVPN configurate.
    Vedere *Verifica dello stato di OpenVPN* `**Clienti e
    server** <#_bookmark468>`__.

    **Registro dei pacchetti** Visualizza i log da alcuni pacchetti
    supportati.

    **Code** Mostra lo stato delle code che modellano il traffico.
    Vedere\ *Monitoraggio delle code*.

    **Servizi** Mostra lo stato dei demoni del sistema e del servizio
    pacchetti. Vedere\ *Stato del servizio*.

    **Registri di sistema** Mostra i registri del sistema e i servizi di
    sistema come firewall, DHCP, VPN, ecc. Vedere *Registri di sistema*.

    **Grafico del traffico** Visualizza un grafico del traffico dinamico
    in tempo reale per un'interfaccia. Vedere\ *Grafici del traffico*.

    **UPnP e NAT-PMP** Mostra un elenco di qualsiasi porta UPnP
    attualmente attiva. Questa voce è presente solo quando il firewall
    contiene più di un'interfaccia. Vedere\ *UPnP e NAT-PMP*.

    **Wireless** Mostra un elenco di tutte le reti wireless attualmente
    disponibili nel raggio d'azione, insieme ai livelli del segnale.
    Questa voce di menu è presente solo se al firewall è assegnata
    un'interfaccia wireless. Vedere\ *Controllare lo stato del wireles*.

Diagnostica
'''''''''''

Le voci nel menu **Diagnostica** eseguono varie attività diagnostiche e
amministrative.

    **Tabella ARP** Visualizza un elenco di dispositivi visti localmente
    dal firewall. L'elenco include un indirizzo IP, un indirizzo MAC, un
    nome host, l'interfaccia in cui è stato visualizzato il dispositivo
    e altre informazioni correlate.

    **Autenticazione** Verifica l'autenticazione su un server RADIUS o
    LDAP definito. Vedere *Risoluzione dei problemi*.

    **Backup e ripristino** Backup e ripristino dei file di
    configurazione. Vedere *Backup e ripristino*.

    **Prompt dei comandi** Esegue i comandi della shell o il codice PHP
    e carica/scarica i file sul/dal firewall. Usare con cautela.

    **Ricerca DNS** Esegue una ricerca DNS per risolvere i nomi host a
    fini diagnostici e per testare la connettività ai server DNS. Vedere
    *Testare il DNS*.

    **Modifica del file** Modifica un file sul filesystem del firewall.

    **Impostazioni di fabbrica** Ripristina la configurazione ai valori
    predefiniti. Tenere presente, tuttavia, che ciò non altera il
    filesystem o disinstalla i file del pacchetto; cambia solo le
    impostazioni di configurazione. Vedere *Ripristinare le impostazioni
    di fabbrica predefinite*.

    **Mirror GEOM** Se il firewall contiene un mirror del disco GEOM,
    questa pagina mostra lo stato del mirror e fornisce i controlli per
    la gestione del mirror.

    **Sistema di arresto** Chiude il firewall e disattiva
    l'alimentazione ove possibile. Vedere *Sistema di arresto*.

    **Informazioni sul limitatore** Mostra lo stato di tutti i
    limitatori e il traffico che scorre al loro interno. Vedere
    *Controllo dell’uso del limitatore*.

    **Tabella NDP** Mostra un elenco di dispositivi IPv6 locali visti
    dal firewall. L'elenco include un indirizzo IPv6, un indirizzo MAC,
    un nome host (se noto al firewall) e l'interfaccia.

    **Acquisizione pacchetti** Esegue un'acquisizione di pacchetti per
    ispezionare il traffico, quindi visualizzare o scaricare i
    risultati. Vedere *Acquisizione di pacchetti dalla WebGUI*.

    **PFInfo** Visualizza le statistiche sul filtro pacchetti, inclusi i
    tassi di traffico generali, i tassi di connessione, le informazioni
    sulla tabella di stato e vari altri contatori. Vedere *PFInfo*.

    **pfTop** Visualizza un elenco delle principali connessioni attive
    in base a una metrica selezionabile come byte, frequenza, età, ecc.
    Vedere *Visualizzazione degli stati con pfTop*.

    **ping** Invia richieste di eco ICMP a un determinato indirizzo IP,
    inviato tramite un'interfaccia scelta.

    **Riavvio del sistema** Riavvia il firewall. Il completamento
    dell'operazione può richiedere alcuni minuti, a seconda
    dell'hardware e delle funzionalità abilitate. Vedere *Riavvio del
    sistema*.

    **Itinerari** Mostra i contenuti della tabella di routing. Vedere
    *Visualizzazione dei percorsi*.

    **Stato SMART** Visualizza le informazioni diagnostiche sulle unità
    disco, se supportate dall'hardware. Può anche eseguire test di
    guida. Vedere *Stato del disco rigido SMART*.

    **Sockets** Visualizza un elenco di processi sul firewall che sono
    collegati alle porte di rete, ascoltando le connessioni o
    effettuando connessioni in uscita dal firewall stesso.

    **Stati** Mostra gli stati del firewall attualmente attivi. Vedere
    *Stati del firewall*.

    **Riepilogo degli stati** Visualizza le informazioni sulla tabella
    di stato, per visualizzare le attività riepilogate per indirizzo IP.
    Vedere *Riepilogo degli stati*.

    **Attività di sistema** Mostra l'utilizzo della memoria e un elenco
    di processi attivi e thread di sistema sul firewall, l'output
    proviene da top -aSH. Vedere *Attività di sistema (in alto)*.

    **Tabelle** Visualizza e modifica i contenuti di varie tabelle e
    alias firewall. Vedere *Visualizzazione dei contenuti di*
    `**tabelle** <#_bookmark671>`__.

    **Porta di prova** Esegue un semplice test di connessione TCP dal
    firewall per determinare se un host remoto sta accettando
    connessioni su una porta specifica.

    **Traceroute** Traccia il percorso seguito dai pacchetti tra questo
    firewall e un sistema remoto. Vedere *Utilizzando*
    `**traceroute** <#_bookmark299>`__.

Questa sezione è una guida alle scelte di menu standard disponibili in
|firew4ll|. Questa guida aiuterà a identificare rapidamente lo scopo di una
determinata opzione di menu e fare riferimento ai luoghi del libro in
cui tali opzioni sono discusse in modo più dettagliato.

I pacchetti possono aggiungere elementi a qualsiasi menu, quindi
controllare ogni menu o consultare la documentazione di un pacchetto per
individuare le voci del menu. In genere, i pacchetti installano le voci
nel menu Servizi, ma ci sono numerose eccezioni.
