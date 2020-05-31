********************
Gestione Certificati
********************

Gestione dell’autorità dei certificati
''''''''''''''''''''''''''''''''''''''

Le autorità di certificazione (CA) sono gestite da **Sistema>Gestione
certificati**, nella scheda **CA**. Da questa schermata i CA possono
essere aggiunti, modificati, esportati o cancellati.

Creare una nuova autorità di certificazione
===========================================

Per creare una nuova CA, avviare il processo come segue:

-  Passare a **Sistema>Gestione certificazioni** nella scheda **CA**.

-  Fare clic su **Aggiungere** per creare una nuova CA.

-  Inserire un **nome descrittivo** per la CA. Questo è usato come
   etichetta per questa CA in tutta la GUI.

-  Selezionare il metodo che meglio si adatti a come verrà generata la
   CA. Queste opzioni e ulteriori istruzioni sono nelle sezioni
   corrispondenti qui sotto:

   -  Creare un'autorità di certificazione interna

   -  Importare un'autorità di certificazione esistente

   -  Creare un'autorità di certificazione intermedia

Creare un'autorità di certificazione interna
--------------------------------------------

Il metodo più comune utilizzato da qui è quello di creare un'autorità di certificazione interna. Questo farà una nuova CA di root basata sulle informazioni inserite in questa pagina.

-  Selezionare la **lunghezza della chiave** per scegliere come "forte"
   la CA è in termini di crittografia. Più lunga è la chiave, più sicura
   è. Tuttavia, i tasti più lunghi possono richiedere più tempo alla CPU
   per essere processati, quindi non è sempre saggio usare il valore
   massimo. Il valore predefinito di *2048* è un buon equilibrio.

-  Selezionare un **algoritmo Digest** dall'elenco fornito. La migliore
   pratica attuale è usare un algoritmo più forte di SHA1, dove
   possibile. *SHA256* è una buona scelta.

	-.. note:: 
		Alcune apparecchiature più vecchie o meno sofisticate, come ad esempio telefoni VoIP abilitati-VPN possono supportare solo SHA1 per l'algoritmo Digest. Consultare la documentazione del dispositivo per le specifiche.

-  Digitare un valore di durata di vita per specificare il numero di
   giorni per i quali la CA sarà valida. La durata dipende dalle
   preferenze personali e le politiche del sito. Cambiare la CA spesso è
   più sicuro, ma è anche un problema di gestione in quanto
   richiederebbe la riedizione di nuovi certificati alla scadenza della
   CA. Per impostazione predefinita la GUI suggerisce di utilizzare 3650
   giorni, che è di circa 10 anni.

-  Digitare i valori per la sezione **Nome distinto** per i parametri
   personalizzati nella CA. Questi sono tipicamente riempiti con le
   informazioni di un'organizzazione, o nel caso di un individuo, le
   informazioni personali. Queste informazioni sono per lo più
   cosmetiche, utilizzate per verificare l'esattezza della CA e per
   distinguere l'CA dall'altra. Non devono essere utilizzati segni di
   punteggiatura e caratteri speciali.

   -  Selezionare il **codice del paese** dall'elenco. Questo è il
      codice del paese riconosciuto-ISO, non un dominio di primo livello
      con nome host.

   -  Indicare lo **Stato** o la **provincia** in modo completo, non
      abbreviato.

   -  Inserire la **città**.

   -  Indicare il nome dell'\ **organizzazione**, in genere il nome
      della società.

   -  Inserire un **indirizzo email** valido.

   -  Inserire il **nome comune** (CN). Questo campo è il nome interno
      che identifica la CA. A differenza di un certificato, il CN per
      una CA non ha bisogno di essere il nome host, o qualcosa di
      specifico. Ad esempio, potrebbe essere chiamato *VPNCA* o *MiaCA*.

.. note:: Anche se è tecnicamente valido, evitare l'uso di spazi nel CN.

-  Fare clic su **Salvare**

Se vengono segnalati errori, ad esempio caratteri non validi o altri
problemi di input, saranno descritti sullo schermo. Correggere gli
errori, e tentare di salvare di nuovo.

Importa un'autorità di certificazione esistente
-----------------------------------------------

Se una CA esistente proveniente da una fonte esterna deve essere
importata, è possibile farlo selezionando il **metodo** di *importazione
di un'autorità di certificazione esistente*. Questo può essere utile in
due modi: uno, per le CA realizzate utilizzando un altro sistema, e due,
per le CA fatte da altri che devono essere affidabili.

-  Inserire i **dati del certificato** per la CA. Per avere fiducia in
   una CA proveniente da un'altra fonte, sono richiesti solo i dati del
   certificato per la CA. È tipicamente contenuto in un file che termina
   con *. crt* o *.pem*. Sarebbe testo semplice, e racchiuso in un
   blocco come:

	.. code-block:: none
		-----BEGIN CERTIFICATE-----
		[A bunch of random-looking base64-encoded data]
		-----END CERTIFICATE-----``

-  Inserire la chiave di certificazione privata se si importa una CA
   esterna personalizzata, o una CA che è in grado di generare i propri
   certificati e liste di revoca dei certificati. Questo è tipicamente
   in un file che termina in *.key*. Sarebbero dati di testo semplice
   racchiusi in un blocco come

	.. code-block:: none
		-----BEGIN RSA PRIVATE KEY-----
		[A bunch of random-looking base64-encoded data]
		-----END RSA PRIVATE KEY-----


-  Inserire il **Seriale** per il prossimo certificato se la chiave
   privata è stata inserita. Questo è essenziale. Una CA creerà
   certificati ciascuno con un numero di serie unico in sequenza. Questo
   valore controlla la seriale del prossimo certificato generato da
   questa CA. È essenziale che ogni certificato abbia una serie unica, o
   ci saranno problemi in seguito con la revoca del certificato. Se il
   prossimo seriale è sconosciuto, cercare di stimare quanti certificati
   sono stati fatti dalla CA, e poi impostare il numero abbastanza alto
   perché una collisione sia improbabile.

-  Fare clic su **Salvare**

Se vengono segnalati errori, ad esempio caratteri non validi o altri
problemi di input, saranno descritti sullo schermo. Correggere gli
errori, e tentare di salvare di nuovo.

Importazione di un'autorità di certificazione a catena o a nidificazione
------------------------------------------------------------------------

Se la CA è stata firmata da un intermediario e non direttamente da un CA
di root, può essere necessario importare insieme la CA di root e quella
intermedia in un'unica voce, come:

	.. code-block:: none
		-----BEGIN CERTIFICATE-----
		[Subordinate/Intermediate CA certificate text]
		-----END CERTIFICATE-----
		-----BEGIN CERTIFICATE-----
		[Root CA certificate text]
		-----END CERTIFICATE-----

Creare un'autorità di certificazione intermedia
-----------------------------------------------

Una CA intermedia creerà una nuova CA in grado di generare certificati,
ma dipende da un'altra CA superiore ad essa. Per crearne uno,
selezionare *Creare un'autorità di certificazione intermedia* dal menu a
discesa **Metodo**.

.. note:: Il CA di livello superiore deve essere già presente su |firew4ll| (Creato o importato)

-  Scegliere l'CA di livello superiore per firmare questa CA utilizzando
   l’elenco a discesa **Firmare l’autorità di certificazione**. Verranno
   mostrate solo le CA con chiavi private presenti, in quanto ciò è
   necessario per firmare correttamente questa nuova CA.

-  Inserire i parametri rimanenti identici a quelli per la *creazione di
   un'autorità di certificazione interna*.

Modifica di un'autorità di certificazione
=========================================

Dopo l'aggiunta di una CA, può essere modificata dall'elenco delle CA
presenti nella **scheda Sistema>Gestione certificazioni** sulla scheda
**CA**. Per modificare una CA, fare clic sull'icona |image0| alla fine
della riga. Lo schermo presentato permette di modificare i campi come se
la CA fosse stata importata.

Per informazioni sui campi in questa schermata, vedere *Importare
un'autorità di certificazione esistente*. Nella maggior parte dei casi
lo scopo di questa schermata sarebbe quello di correggere il **Seriale**
della CA, se necessario, o di aggiungere una chiave ad una CA importata
in modo che possa essere utilizzata per creare e firmare certificati e
CRL.

Esportare un’autorità di certificato
====================================

Dall'elenco delle CA di **Sistema>Gestione certificati** nella scheda
**CA**, è possibile esportare il certificato e/o la chiave privata di
una CA. Nella maggior parte dei casi la chiave privata di una CA non
verrebbe esportata, a meno che non si stia trasferendo in una nuova sede
o si stia effettuando un backup. Quando si utilizza la CA per una VPN o
per altri scopi, esportare solo il certificato per la CA.

.. warning::
	Se la chiave privata di una CA entra nelle mani sbagliate, l'altra parte potrebbe generare nuovi certificati che sarebbero considerati validi contro la CA.

Per esportare il certificato per una CA, fare clic sull'icona |image1| a
sinistra. Per esportare la chiave privata per la CA, fare clic
sull'icona |image2| a destra. Spostare il puntatore del mouse sull'icona
e un suggerimento mostrerà l'azione da eseguire per una facile conferma.
I file verranno scaricati con il nome descrittivo della CA come nome del
file, con l'estensione *.crt* per il certificato, e *.key* per la chiave
privata.

Rimuovere un'autorità di certificazione
=======================================

Per rimuovere una CA, prima deve essere rimossa dal servizio attivo.

-  Controllare le aree che possono utilizzare una CA, come OpenVPN,
   IPsec, e pacchetti.

-  Rimuovere le voci che utilizzano la CA o selezionare una diversa CA.

-  Passare a **Sistema>Gestione certificati** nella scheda **CA**.

-  Trovare la **CA** per eliminarla nell'elenco.

-  Cliccare su |image3| alla fine della riga per la CA.

-  Cliccare OK nella finestra di conferma.

Se viene visualizzato un errore, seguire le istruzioni sullo schermo per
correggere il problema e quindi riprovare.

Gestione certificati
''''''''''''''''''''

I certificati sono gestiti dal **Sistema>Gestione certificati**, nella
scheda **Certificati**. Da questa schermata i certificati possono essere
aggiunti, modificati, esportati o cancellati.

Creare un nuovo certificato
===========================

Per creare un nuovo certificato, avviare il processo nel modo seguente:

-  Passare a **Sistema>Gestione certificati** nella scheda
   **Certificati**.

-  Fare clic su **Aggiungere** per creare un nuovo certificato.

-  Immettere un **nome descrittivo** per il certificato. Questo è usato
   come etichetta per questo certificato per tutta la GUI.

-  Selezionare il **metodo** che meglio si adatta a come verrà generato
   il certificato. Queste opzioni e ulteriori istruzioni sono nelle
   relative sezioni di seguito:

   -  Importazione di un certificato esistente

   -  Creare un certificato interno

   -  Creare un Richiesta di firma del certificato

Importazione di un certificato esistente
----------------------------------------

Se un certificato esistente proveniente da una fonte esterna deve essere
importato, può essere fatto selezionando il metodo di importazione di un
certificato esistente. Questo può essere utile per i certificati che
sono stati effettuati utilizzando un altro sistema o per i certificati
che sono stati forniti da un terzo.

-  Inserire i dati del certificato, questo è richiesto. È tipicamente
   contenuto in un file che termina con *.crt*. Sarebbe un testo
   semplice, e racchiuso in un blocco come:
   .. code-block:: none
		-----BEGIN CERTIFICATE-----
		[A bunch of random-looking base64-encoded data]
		-----END CERTIFICATE-----

-  Inserire i dati della **chiave privata** è anche necessario. Questo è
   in genere in un file con estensione *.key*
   .. code-block:: none
		-----BEGIN RSA PRIVATE KEY-----
		[A bunch of random-looking base64-encoded data]
		-----END RSA PRIVATE KEY-----

-  Cliccare su Salvare per completare il processo di importazione.

Se si verificano errori, seguire le istruzioni sullo schermo per
risolverli. L'errore più comune è non incollare nella giusta parte del
certificato o della chiave privata. Assicurasi di includere l'intero
blocco, tra cui l'intestazione e il piè di pagina intorno i dati
codificati.

Creare un certificato interno
=============================

Il **metodo** più comune è creare un certificato interno. Questo creerà
un nuovo certificato utilizzando una delle autorità di certificazione
esistente.

-  Selezionare l'\ **autorità di certificazione** con cui verrà firmato
   il presente certificato. Solo una CA che ha una chiave privata
   presente può essere in questo elenco, in quanto la chiave privata è
   necessaria per la CA per firmare un certificato..

-  Selezionare la **lunghezza della chiave** per scegliere come "forte"
   il certificato è in termini di crittografia. Più lunga è la chiave,
   più sicura è. Tuttavia, i tasti più lunghi possono richiedere più
   tempo alla CPU per essere processati, quindi non è sempre saggio
   usare il valore massimo. Il valore predefinito di *2048* è un buon
   equilibrio..

-  Selezionare un **algoritmo Digest** dall'elenco fornito. La migliore
   pratica attuale è usare un algoritmo più forte di SHA1, dove
   possibile. *SHA256* è una buona scelta.

.. note:: Alcune apparecchiature più vecchie o meno sofisticate, come ad esempio telefoni VoIP VPN abilitati possono supportare solo SHA1 per l'algoritmo Digest. Consultare la documentazione del dispositivo per le specifiche.

-  Selezionare un **tipo di certificato** che corrisponda allo scopo del
   presente certificato.

   -  Scegliere un **Certificato del server** se il certificato verrà
      utilizzato in un server VPN o server HTTPS. Questo indica ciò che
      all'interno del certificato può essere utilizzato in un ruolo di
      server, e nessun altro.

.. note:: I certificati tipo server includono attributi dell’uso della chiave estesa che indicano che possono essere utilizzati per l'autenticazione del server così come l'OID 1.3.6.1.5.5.8.2.2 che viene utilizzato da Microsoft per significare che un certificato può essere utilizzato come intermediario IKE. Questi sono necessari per Windows 7 e successivamente per fidarsi del certificato del server per l'uso con alcuni tipi di VPN. Essi sono anche contrassegnati con un vincolo che indica che non sono una CA, e hanno impostato nsCertType su "server". 

-  Scegliere **Certificato utente** se il certificato può essere
   utilizzato in una capacità dell’utente finale, come un client VPN, ma
   non può essere utilizzato come server. Questo impedisce all'utente di
   usare il proprio certificato per impersonare un server.

.. note:: I certificati di tipo utente includono attributi dell’uso della chiave estesa che indicano che possono essere utilizzati per l'autenticazione del client. Essi sono inoltre contrassegnati da un vincolo che indica che non si tratta di una CA.

-  Scegliere l'\ **autorità di certificazione** per creare una CA
   intermedia. Un certificato generato in questo modo sarà subordinato
   alla CA scelta. Può creare i propri certificati, ma la CA della root
   deve anche essere inclusa quando viene usata. Questo è noto anche
   come "incatenamento"

-  Digitare un valore di **durata di vita** per specificare il numero di
   giorni per i quali il certificato sarà valido. La durata dipende
   dalle preferenze personali e le politiche del sito. Cambiare il
   certificato spesso è più sicuro, ma è anche un problema di gestione
   in quanto richiede la riedizione di nuovi certificati quando scadono.
   Per impostazione predefinita la GUI suggerisce di utilizzare 3650
   giorni, che sono circa 10 anni.

-  Digitare i valori per la sezione **Nome distinto** per i parametri
   personalizzati nel certificato. La maggior parte di questi campi
   saranno pre-popolati con i dati della CA. Tali informazioni sono
   generalmente fornite con le informazioni di un'organizzazione, o nel
   caso di un individuo, informazioni personali. Queste informazioni
   sono per lo più cosmetiche, utilizzate per verificare l'esattezza del
   certificato e per distinguere un certificato da un altro. Non devono
   essere utilizzati segni di punteggiatura e caratteri speciali.

   -  Selezionare il **codice paese** dalla lista. Questo è il codice
      ISO del paese riconosciuto, non un dominio di livello superiore
      con nome host.

   -  Inserire lo **Stato** o **Provincia** scritto per intero, non
      abbreviato.

   -  Inserire la **città**.

   -  Inserire il nome dell'\ **organizzazione**, in genere il nome
      della società.

   -  Inserire un **indirizzo email** valido.

   -  Inserire il **nome comune** (CN). Questo campo è il nome interno
      che identifica il certificato. A differenza di una CA, il CN per
      un certificato dovrebbe essere un nome utente o nome dell’host. Ad
      esempio, potrebbe essere chiamato *certificatoVPN*, *utente01*, o
      *vpnrouter.esempio.com*.

.. note:: Anche se è tecnicamente valido, evitare l'uso di spazi nel CN.

-  Fare clic su |image4| **Aggiungere** per **Aggiungere nomi
   alternativi** se necessari. I nomi alternativi consentono al
   certificato di specificare più nomi che sono tutti validi per il NC,
   come due nomi host diversi, un indirizzo IP aggiuntivo, un URL, o un
   indirizzo e-mail. Questo campo può essere lasciato vuoto se non è
   richiesto o se il suo scopo non è chiaro.

   -  Inserire un **Tipo** per il nome alternativo. Questo deve
      contenere uno dei *DNS* (FQDN o nome host), *IP* (indirizzo IP),
      *URI*, o *e-mail*.

   -  Immettere un **Valore** per il Nome alternativo. Questo campo deve
      contenere un valore opportunamente formattato in base al tipo
      immesso.

   -  Cliccare |image5| **Eliminare** alla fine della riga per un Nome
      alternativo non necessario.

   -  Ripetere questa procedura per ogni ulteriore **Nome alternativo**.

-  Fare clic su **Salvare**

Se vengono segnalati errori, come caratteri non validi o altri problemi
di input, essi saranno descritti sullo schermo. Correggere gli errori e
tentare di salvare di nuovo.

Crea una richiesta di firma del certificato
-------------------------------------------

La scelta di un **metodo** di *richiesta di firma di certificato* crea
un nuovo file di richiesta che può essere inviato a una CA di terze
parti da firmare. Questo dovrebbe essere utilizzato per ottenere un
certificato da un'autorità di certificazione root di fiducia. Una volta
scelto questo metodo, i parametri rimanenti per la creazione di questo
certificato sono identici a quelli per la *creazione di un certificato
interno*.

Esportare un certificato
========================

Dall'elenco dei certificati di **Sistema>Gestione certificati** nella
scheda **Certificati**, un certificato e/o la sua chiave privata possono
essere esportati.

Per esportare il certificato, fare clic sull'icona |image6|. Per
esportare la chiave privata del certificato, fare clic sull'icona
|image7|. Per esportare il certificato della CA, il certificato e la
chiave privata per il certificato insieme in un file PKCS#12, fare clic
sull'icona |image8|. Per confermare l'esportazione del file corretto,
posizionare il puntatore del mouse sull'icona e un suggerimento mostrerà
l'azione da eseguire.

I file verranno scaricati con il nome descrittivo del certificato come
nome del file, e l'estensione *.crt* per il certificato e *.key* per la
chiave privata, o *. P12* per un file PKCS#12.

Rimuovere un certificato
========================

Per rimuovere un certificato, prima deve essere rimosso dall'uso attivo.

-  **Selezionare** le aree che possono utilizzare un certificato, come
   ad esempio le opzioni di WebGUI, OpenVPN, IPsec, e pacchetti.

-  Rimuovere le voci utilizzando il certificato, oppure scegliendo un
   altro certificato.

-  Passare a **Sistema>Gestione certificati** nella scheda
   **Certificati**.

-  Individuare il certificato da eliminare nella lista

-  Cliccare su |image9| alla fine della riga per il certificato.

-  Fare clic su OK nella finestra di conferma.

Se viene visualizzato un errore, seguire le istruzioni sullo schermo per
correggere il problema e quindi riprovare.

Certificati dell’utente
=======================

Se viene utilizzata una VPN che richiede certificati utente, essi
possono essere creati in uno dei diversi modi. Il metodo esatto dipende
da dove viene eseguita l'autenticazione per la VPN e se il certificato
esiste già o meno.

Nessuna autenticazione o autenticazione esterna
-----------------------------------------------

Se non c'è un'autenticazione utente, o se l'autenticazione utente viene
eseguita su un server esterno (RADIUS, LDAP, ecc) allora fare un
certificato utente come qualsiasi altro certificato descritto in
precedenza. Assicurarsi che il certificato utente sia selezionato per il
tipo di certificato e che il nome comune sia il nome utente dell'utente.

Autenticazione locale/Creare certificato quando si crea un utente
-----------------------------------------------------------------

Se l'autenticazione utente viene eseguita su |firew4ll|, il certificato
utente può essere fatto all'interno della gestione degli utenti.

-  Passare a **Sistema>Gestione utenti**

-  Creare un utente. Vedere *Gestione utenti e autenticazione* per
   dettagli.

-  Compilare il **nome utente** e la **password**

-  Selezionare **Fare clic per creare un certificato utente** nella
   sezione certificati utente, che mostrerà una forma semplice per la
   creazione di un certificato utente.

   -  Inserire una breve **Nome descrittivo**, che può essere il nome
      utente o qualcosa come *accesso remoto al certificato della VPN di
      Bob*.

   -  Scegliere l'\ **autorità di certificazione** adeguata per la VPN.

   -  Regolare la **lunghezza della chiave** e **la durata di vita** se
      lo si desidera.

-  Finire gli altri dettagli utente necessari.

-  Fare clic su **Salvare**

Autenticazione locale/aggiungere un certificato a un utente esistente
---------------------------------------------------------------------

Per aggiungere un certificato a un utente esistente:

-  Passare a **Sistema> Gestione utenti**

-  Cliccare su |image10| per modificare l'utente

-  Cliccare su |image11| **Aggiungere** sotto i certificati utente.

-  Scegliere le opzioni disponibili in base alle esigenze del processo
   di creazione del certificato descritto in *Creare un nuovo
   certificato*, o selezionare *Scegliere un certificato esistente* e
   quindi selezionare uno dei **certificati esistenti**

Per ulteriori informazioni su come aggiungere e gestire utenti, vedere
*Gestione utenti e autenticazione*.

Gestione degli elenchi di revoca dei certificati
''''''''''''''''''''''''''''''''''''''''''''''''

Le liste di revoca dei certificati (CRL) fanno parte del sistema X.509
che pubblica elenchi di certificati che non dovrebbero più essere
attendibili. Tali certificati possono essere stati compromessi o essere
altrimenti invalidati. Un'applicazione che utilizza una CA, come
OpenVPN, può opzionalmente utilizzare una CRL in modo da poter
verificare i certificati dei client di connessione. Una CRL è generata e
firmata contro una CA utilizzando la sua chiave privata, quindi per
creare o aggiungere certificati a una CRL nella GUI, la chiave privata
della CA deve essere presente. Se la CA è gestita esternamente e la
chiave privata per la CA non è sul firewall, una CRL può ancora essere
generata al di fuori del firewall e importata.

Il modo tradizionale di utilizzare una CRL è quello di avere solo una
CRL per CA e solo aggiungere certificati non validi a tale CRL. In
|firew4ll|, tuttavia, possono essere create più CRL per una singola CA. In
OpenVPN, possono essere scelte diverse CRL per istanze VPN separate. Ciò
potrebbe essere utilizzato, ad esempio, per impedire ad un certificato
specifico di connettersi ad un'istanza mentre gli consente di collegarsi
ad un'altra. Per IPsec, tutte le CRL sono consultate e non c'è nessuna
selezione come attualmente esiste con OpenVPN.

Le liste di revoca dei certificati sono gestite da **Sistema>Gestione
certificati**, nella scheda **Revoca dei certificati**. Da questa
schermata le voci della CRL possono essere aggiunte, modificate,
esportate o cancellate. L'elenco mostrerà tutte le autorità di
certificazione e un'opzione per aggiungere una CRL. Lo schermo indica
anche se la CRL è interna o esterna (importata) e mostra il numero di
certificati revocati su ciascuna CRL.

.. note:: Le CRL generate con |firew4ll| 2.2.4-RELEASE e versioni
successive includono l'attributo identificativo della chiave
amministrativa per consentire la corretta funzionalità con strongSwan
per l'uso con IPsec.

Creare una nuova lista di revoca dei certificati
================================================

Per creare una nuova CRL:

-  Passare a Sistema>Gestione certificati, nella scheda revoca dei
   certificati.

-  Trovare la riga con la CA per cui la LCR verrà creata.

-  Cliccare |image12| **Aggiungere** o **Importare la CRL** alla fine
   della riga per creare una nuova CRL.

-  Scegli **Creare una lista di revoche di certificato interna** per il
   **metodo**.

-  Inserire un **nome descrittivo** per la CRL, che viene utilizzato per
   identificare questa CRL nelle liste in tutta la GUI. Di solito è
   meglio includere un riferimento al nome della CA e/o lo scopo della
   CRL.

-  Selezionare la CA appropriata dal menu a discesa delle **Autorità di
   certificazione**.

-  Inserire il numero di giorni per i quali la CRL dovrebbe essere
   valida nella casella della **durata di vita**. Il valore di default è
   *9999*

-  giorni, o anni quasi 27 e mezzo.

   -  Fare clic su **Salvare**

Il browser farà ritorno alla lista CRL, e la nuova voce verrà mostrata
lì.

Importare una lista di revoca dei certificati esistenti
=======================================================

Per importare una CRL da una fonte esterna:

-  Passare a **Sistema>Gestione certificati**, nella scheda di **revoche
   di certificati**

-  Trovare la riga con la CA per cui la LCR sarà importata.

-  Cliccare su |image13| **Aggiungere** o **Importare la CRL** alla fine
   della riga per creare una nuova CRL.

-  Selezionare **Importare una lista della revoca dei certificati
   esistente** per il **metodo**.

-  Inserire un **nome descrittivo** per la CRL, che viene utilizzata per
   identificare questa CRL nelle liste in tutta la GUI. Di solito è
   meglio includere un riferimento al nome della CA e/o lo scopo della
   CRL.

-  Selezionare la CA appropriata dal menu a discesa **Autorità di
   certificazione**.
	.. code-block::
		-----BEGIN X509 CRL-----
		[A bunch of random-looking base64-encoded data]
		-----END X509 CRL-----


-  Inserire i **dati della CRL**. Questo è di solito in un file che
   termina in *.crl*. Sarebbero dati di testo semplice racchiusi in un
   blocco come:

-  Fare clic su **Salvare** per completare il processo di importazione.

Se appare un errore, seguire le istruzioni sullo schermo per correggere
il problema e quindi riprovare. L'errore più comune è non incollare
nella parte giusta dei dati della CRL. Accertarsi di inserire l'intero
blocco, compresi l'intestazione iniziale e il piè di pagina finale dei
dati codificati.

Esportare una lista di revoche di certificati
=============================================

Dall'elenco della CRL di **Sistema>Gestione certificazioni** nella
scheda **Revoca del certificato** può essere esportata anche una CRL.
Per esportare la CRL, fare clic sull'icona |image14|. Il file verrà
scaricato con il nome descrittivo della CRL come il nome del file, e
l'estensione *.crl*.

Eliminare un elenco di revoche di certificati
=============================================

-  Controllare le aree che possono utilizzare la CRL, come OpenVPN.

-  Rimuovere le voci utilizzando la CRL, o scegliere un'altra CRL.

-  Passare a **Sistema>Gestione certificazione** nella scheda **revoca
   dei certificati**.

-  Individuare la CRL per eliminare nell'elenco

-  Cliccare sull’icone |image15| alla fine della riga della CRL.

-  Fare clic su OK nella finestra di conferma.

Se viene visualizzato un errore, seguire le istruzioni sullo schermo per
correggere il problema e quindi riprovare.

Revocare un certificato
=======================

Una CRL non è molto utile se non contiene certificati revocati. Un
certificato viene revocato aggiungendolo in una CRL:

-  Passare a **Sistema>Gestione certificati** nella scheda **revoca dei
   certificati**.

-  Individuare la CRL da modificare nella lista

-  Cliccare l’icona |image16| alla fine della riga della CRL. Verrà
   presentata una schermata che elenca tutti i certificati attualmente
   revocati, e un controllo per aggiungerne di nuovi.

-  Selezionare il certificato dalla lista **Scegliere un certificato da
   revocare**.

-  Selezionare un **motivo** dall'elenco a discesa per indicare il
   motivo per cui il certificato è stato revocato. Queste informazioni
   non pregiudicano la validità del certificato, sono semplicemente di
   natura informativa. Questa opzione può essere lasciata al valore di
   default.

-  Fare clic su **Aggiungere** e il certificato verrà aggiunto alla CRL.

   I certificati possono essere rimossi dalla CRL utilizzando pure
   questa schermata:

-  Passare a **Sistema>Gestione certificati** nella scheda **revoca dei
   certificati**.

-  Individuare la CRL da modificare nella lista

-  Cliccare l’icona |image17| alla fine della riga della CRL.

-  Trovare il certificato nell'elenco e fare clic sull’icona |image18|
   per rimuoverlo dalla CRL.

-  Fare clic su **OK** nella finestra di conferma.

Dopo l’aggiunta o la rimozione di un certificato, la CRL sarà ri-scritta
se è attualmente in uso da parte di tutte le istanze della VPN in modo
che i cambiamenti della CRL saranno immediatamente attive.

Aggiornamento di una lista di revoche di certificati importata
==============================================================

Per aggiornare una CRL importata:

-  Passare a **Sistema>Gestione certificati** nella scheda **revoca dei
   certificati**.

-  Individuare la CRL da modificare nella lista

-  Cliccare sull’icona\ |image19| alla fine della riga della CRL.

-  Cancellare il contenuto incollato nella casella dei **dati della
   CRL** e sostituirlo con il contenuto della nuova CRL

-  Fare clic su **Salvare**.

Dopo l'aggiornamento della CRL importata, sarà ri-scritta se è
attualmente in uso da parte di tutte le istanze della VPN in modo che i
cambiamenti della CRL saranno immediatamente attive.

Introduzione di base all'infrastruttura a chiave pubblica X.509
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Un'opzione di autenticazione per le VPN è quella di usare le chiavi
X.509. Una discussione approfondita sulle infrastrutture X.509 e le
chiavi pubblicje (PKI) esula dall'ambito di questo libro ed è
l'argomento di un certo numero di libri interi per gli interessati ai
dettagli. Questo capitolo fornisce la comprensione di base necessaria
per la creazione e la gestione dei certificati in |firew4ll|.

Con le PKI, viene creata prima un'autorità di certificazione (CA).
Questa CA firma poi tutti i singoli certificati nella PKI. Il
certificato della CA viene utilizzato sui server e sui client VPN per
verificare l'autenticità dei certificati server e dei client utilizzati.
Il certificato per la CA può essere utilizzato per verificare la firma
dei certificati, ma non per firmare i certificati. La firma dei
certificati richiede la chiave privata per la CA. La segretezza della
chiave privata della CA è ciò che garantisce la sicurezza di una PKI.
Chiunque abbia accesso alla chiave privata della CA può generare
certificati da utilizzare su una PKI, quindi deve essere mantenuta
sicura. Questa chiave non è mai distribuita a client o server.

.. warning:: Non copiare mai più file sui client di quelli necessari, in quanto questo potrebbe compromettere la sicurezza della PKI.

Un certificato è considerato valido se è attendibile per una data CA.
Nel caso delle VPN, ciò significa che un certificato rilasciato da una
CA specifica sarebbe considerato valido per qualsiasi VPN che utilizza
tale CA. Per questo motivo la migliore pratica è quella di creare una CA
unica per ogni VPN che ha un diverso livello di sicurezza. Per esempio,
se ci sono due VPN di accesso mobile con lo stesso accesso di sicurezza,
usare la stessa CA per quelle VPN è OK. Tuttavia se una VPN è per gli
utenti e un'altra VPN è per la gestione remota, ognuna con restrizioni
diverse, allora dovrebbe essere usata una CA unica per ogni VPN.

Le liste di revoca dei certificati (CRL) sono elenchi di certificati che
sono stati compromessi o che altrimenti devono essere invalidati. La
revoca di un certificato può essere considerata non attendibile a
condizione che l'applicazione che utilizza la CA utilizzi anche una CRL.
Le CRL sono generate e firmate contro una CA utilizzando la sua chiave
privata, quindi per creare o aggiungere certificati a una CRL nella GUI
la chiave privata per una CA deve essere presente.

.. |image0| image:: media/image1.png
   :width: 0.26389in
   :height: 0.26389in
.. |image1| image:: media/image2.png
   :width: 0.26389in
   :height: 0.26389in
.. |image2| image:: media/image3.png
   :width: 0.26389in
   :height: 0.26389in
.. |image3| image:: media/image4.png
   :width: 0.26389in
   :height: 0.26389in
.. |image4| image:: media/image5.png
   :width: 0.26389in
   :height: 0.26389in
.. |image5| image:: media/image4.png
   :width: 0.26389in
   :height: 0.26389in
.. |image6| image:: media/image2.png
   :width: 0.26389in
   :height: 0.26389in
.. |image7| image:: media/image3.png
   :width: 0.26389in
   :height: 0.26389in
.. |image8| image:: media/image6.png
   :width: 0.26389in
   :height: 0.26389in
.. |image9| image:: media/image4.png
   :width: 0.26389in
   :height: 0.26389in
.. |image10| image:: media/image1.png
   :width: 0.26389in
   :height: 0.26389in
.. |image11| image:: media/image5.png
   :width: 0.26389in
   :height: 0.26389in
.. |image12| image:: media/image5.png
   :width: 0.26389in
   :height: 0.26389in
.. |image13| image:: media/image5.png
   :width: 0.26389in
   :height: 0.26389in
.. |image14| image:: media/image7.png
   :width: 0.26389in
   :height: 0.26389in
.. |image15| image:: media/image4.png
   :width: 0.26389in
   :height: 0.26389in
.. |image16| image:: media/image1.png
   :width: 0.26389in
   :height: 0.26389in
.. |image17| image:: media/image1.png
   :width: 0.26389in
   :height: 0.26389in
.. |image18| image:: media/image4.png
   :width: 0.26389in
   :height: 0.26389in
.. |image19| image:: media/image1.png
   :width: 0.26389in
   :height: 0.26389in
