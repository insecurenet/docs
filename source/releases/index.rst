**PREFAZIONE**

Avviso sul Copyright
====================

Copyright © 2019 Electric Sheep Fencing LLC

Ringraziamenti
==============

Questo libro, e il progetto pfSense stesso, non sarebbero possibili
senza un grande team di sviluppatori, contributori, sostenitori
aziendali e una meravigliosa comunità. Il progetto ha ricevuto
contributi per il codice da oltre 200 persone. Centinaia hanno
contribuito finanziariamente per l'hardware e altre risorse necessarie.
Altre migliaia hanno fatto la loro parte supportando il progetto
aiutando gli altri sulla mailing list, sul forum e su altre piattaforme.
E ancora di più hanno contribuito acquistando hardware, supporto e
servizi come l'abbonamento pfSense Gold. I nostri ringraziamenti vanno a
tutti coloro che hanno fatto la loro parte per rendere il progetto il
grande successo che è diventato.

Sviluppatori di pfSense
-----------------------

Ci sono un gran numero di membri del progetto e della comunità, attuali
e passati, che hanno contribuito al progetto, e li ringraziamo tutti!
Questi che seguono non sono elenchi completi e sono presentati in nessun
ordine particolare.

L'attuale team di sviluppo del software pfSense attivo include:

-  Renato Botelho

-  Luiz Otavio O Souza

-  Jim Pingle

-  Jared Dillard

-  Steve Beaver

-  Matthew Smith

Vorremmo anche riconoscere diversi ex membri del progetto che non sono
più contributori attivi:

-  Co-fondatore Chris Buechler

-  Bill Marquette

-  Holger Bauer

-  Erik Kristensen

-  Seth Mos

-  Matthew Grooms

 Insieme a numerosi importanti contributori della comunità, tra cui:

-  Bill Meeks

-  Phil Davis

-  Anthony (BBCan177)

-  Denny Page

-  Piba-NL

-  Marcelloc

-  Stilez

Vorremmo anche ringraziare tutti gli sviluppatori di FreeBSD, in
particolare quelli che hanno assistito in modo considerevole allo
sviluppo del progetto pfSense:

-  Max Laier

-  Christian S.J. Peron

-  Andrew Thompson

-  Bjoern A. Zeeb

-  George Neville-Neil

   1. .. rubric:: Ringraziamenti personali
         :name: ringraziamenti-personali

Da Chris
~~~~~~~~

Devo ringraziare mia moglie e riconoscerle un considerevole merito per
il completamento di questo libro e il successo del progetto in generale.
Questo libro e il progetto hanno portato a innumerevoli giorni, notti e
mesi senza un giorno di pausa e il suo sostegno è stato fondamentale.

Vorrei anche ringraziare le molte aziende che hanno acquistato i nostri
abbonamenti di supporto e i rivenditori che mi hanno permesso di
lavorare a tempo pieno sul progetto all'inizio del 2009.

Devo anche ringraziare Jim per aver partecipato a questo libro e aver
fornito un aiuto considerevole per completarlo. Sono passati due anni e
molto più lavoro di quanto avessi immaginato. sarebbe stato obsoleto
prima che fosse finito se non fosse stato per il suo aiuto negli ultimi
mesi. Inoltre, grazie a Jeremy Reed, il nostro editore e pubblicatore,
per il suo aiuto con il libro.

Infine, i miei ringraziamenti vanno a tutti coloro che hanno contribuito
al progetto pfSense in qualsiasi modo, in particolare agli sviluppatori
che hanno dedicato molto tempo al progetto negli ultimi nove anni.

Da Jim
~~~~~~

Vorrei ringraziare mia moglie e mio figlio, che mi hanno sopportato
durante tutta la mia partecipazione al processo di scrittura non solo
per il primo libro, ma per le continue revisioni nel corso degli anni.
Senza di loro, sarei impazzito molto tempo fa.

Vorrei anche ringraziare Rick Yaney di HPC Internet Services, per essere
di supporto ai software pfSense, FreeBSD e Open Source in generale.

Anche l'intera community di pfSense merita un ringraziamento ancora
maggiore, è il gruppo migliore e più di supporto ad utenti e
contributori di software Open Source che abbia mai incontrato.

Revisori
--------

I seguenti individui hanno fornito feedback e intuizioni indispensabili
per contribuire a migliorare il libro e la sua accuratezza. Elencati in
ordine alfabetico in base al cognome.Jon Bruce

-  Jon Bruce

-  Mark Foster

-  Bryan Irvine

-  Warren Midgley

-  Eirik Øverby

Commenti
========

L'editore e gli autori incoraggiano i commenti per questo libro e la
distribuzione di pfSense. Si prega di inviare suggerimenti, critiche e/o
elogi a The pfSense Book utilizzando i moduli di commento in fondo a
ciascuna pagina o a book@pfsense.org.

Per un feedback generale relativo al progetto pfSense, si prega di
postare sul forum o sulla mailing list. I collegamenti a queste risorse
sono disponibili all'indirizzo
https://www.netgate.com/support/contact-support.html#community-support.

Convenzioni tipografiche
========================

In tutto il libro gli autori usano convenzioni per indicare determinati
concetti, informazioni o azioni. L'elenco seguente fornisce esempi di
come queste vengano utilizzate nel libro

Selezioni del menu Firewall>Regole 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Destinazione delle etichette/nomi degli elementi dell'interfaccia utente grafica (GUI)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pulsanti |image0| Aggiungere
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Prompt per l’inserimento Procedere?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Input dell’utente (testo) Descrizione delle regole
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Input dall’utente (selezione) *WAN* 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nomi del file /riavviare/loader.conf 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nomi dei comandi o programmi gzip 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Comandi digitati nella prompt della shell
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Esempi di riga di comando della shell lunga possono essere suddivisi
utilizzando la (/) per continuare la riga della shell.

Output del comando
~~~~~~~~~~~~~~~~~~

   **Note speciali**

**Nota:** Considerare ciò . . .

.. _section-1:

Attenzione
~~~~~~~~~~

   **Suggerimenti**

**Suggerimento:** La miglior procedura è . . .

Riferimenti
~~~~~~~~~~~

   **Vedere anche:**

   Per maggiori informazioni . . .

L'elenco sopra è un esempio di un "elenco di definizioni" utilizzate per
definire insiemi di termini o opzioni e i loro significati.

Benvenuti nel *libro del pfSense*, scritto dal co-fondatore del progetto
pfSense, Chris Buechler, e dal membro del coreteam, Jim Pingle. Questo
libro tratta argomenti che vanno dal processo di installazione e
configurazione di base alla rete avanzata e firewalling utilizzando
questo firewall open source popolare e la distribuzione del router del
software.

Questo libro è progettato per essere una guida utile per le attività di
rete e di sicurezza comuni insieme a un riferimento completo per le
funzionalità del software pfSense. Il *libro di pfSense* tratta i
seguenti argomenti (e molto altro!):

-  Un'introduzione al software pfSense e alle sue funzionalità.

-  Progettazione del firewall e pianificazione dell'hardware.

-  Installazione e aggiornamento del software pfSense.

-  Utilizzo dell'interfaccia di configurazione basata sul web.

-  Backup e ripristino della configurazione del firewall.

-  Nozioni fondamentali sul firewall, comprese le regole di definizione
      e risoluzione dei problemi.

-  Porta forwarding e Traduzione degli indirizzi di rete (NAT)).

-  Configurazione generale di rete e routing

-  LAN virtuale (VLAN), Multi-WAN e Bridging.

-  Reti private virtuali che utilizzano IPsec e OpenVPN.

-  Shaping del traffico utilizzando ALTQ o Limitatori.

-  Configurazione della rete wireless

-  Impostazione del portale Captive.

-  Alta disponibilità mediante firewall ridondanti.

-  Vari servizi relativi alla rete.

-  Monitoraggio, registrazione, analisi del traffico, sniffing,
      acquisizione dei pacchetti e risoluzione dei problemi del
      firewall.

-  Pacchetti software e installazioni di software di terze parti.

Alla fine di questo libro è presente una *Guida ai menu* con tutte le
opzioni di menu standard disponibili nella Interfaccia Grafica Utente
Web (WebGUI) del software pfSense.

3. .. rubric:: Autori
      :name: autori

   1. .. rubric:: Chris Buechler
         :name: chris-buechler

Uno dei fondatori del progetto pfSense, Chris è stato anche uno dei suoi
sviluppatori più attivi. È stato nel settore IT per oltre un decennio,
lavorando ampiamente con firewall e FreeBSD per la maggior parte del
tempo. Ha fornito servizi di sicurezza, rete e servizi correlati per
organizzazioni del settore pubblico e privato, di dimensioni variabili
da piccole organizzazioni a grandi organizzazioni del settore pubblico e
aziende Fortune 500. Ha conseguito numerose certificazioni del settore
tra cui CISSP, SSCP, MCSE e CCNA tra gli altri. La sua pagina web
personale è disponibile all'indirizzo http://chrisbuechler.com.

Jim Pingle
----------

Jim ha lavorato con FreeBSD per quasi 20 anni e professionalmente negli
ultimi 15 anni. Ora impiegato a tempo pieno di Netgate, fornisce
supporto globale ai software pfSense per i clienti, nonché sviluppo e
documentazione del software. Come ex amministratore di sistema di un ISP
locale a Bedford, Indiana, USA, HPC Servizi Internet, ha lavorato con
server FreeBSD, varie apparecchiature e circuiti di routing e,
naturalmente, firewall basati su pfSense sia internamente che per molti
clienti. Jim si è laureato nel 2002 con una laurea in Sistemi
Informatici presso l'Indiana-Purdue Fort Wayne.

Quando è lontano dal computer, a Jim piace passare il tempo con la sua
famiglia, leggere, giocare a giochi da tavolo e videogiochi, lavorare il
legno, scattare foto e drogarsi di televisione. La sua pagina web
personale è disponibile all'indirizzo
`http: <http://pingle.org/>`__//pingle.org.

.. |image0| image:: media/image1.png
   :width: 0.26389in
   :height: 0.26389in
