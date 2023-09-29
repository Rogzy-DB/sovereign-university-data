---
name: RoninDojo

description: Install and use your RoninDojo Bitcoin node.
---

# Install and use your RoninDojo Bitcoin node.

Running and using your own node is essential to truly participate in the Bitcoin network. While running a Bitcoin node does not bring any financial benefits to the user, it allows them to preserve their privacy, act independently, and have control over their trust in the network.

In this article, we will take a detailed look at RoninDojo, a great solution for running your own Bitcoin node.

### Summary:

- What is RoninDojo?
- What hardware to choose?
- How to install RoninDojo?
- How to use RoninDojo?
- Conclusion

If you are not familiar with how a Bitcoin node works and its role, I recommend starting by reading this article: The Bitcoin Node - Part 1/2: Technical Concepts.

![Samourai](assets/1.png)

## What is RoninDojo?

Dojo is a full Bitcoin node server developed by the Samourai Wallet team. You can freely install it on any machine.

RoninDojo is an installation assistant and administration tool for Dojo and various other tools. RoninDojo takes the original implementation of Dojo and adds many other tools to it, while also making installation and management easier.

They also offer a "plug-and-play" hardware, the RoninDojo Tanto, with RoninDojo pre-installed on a machine assembled by their team. The Tanto is a paid solution, suitable for those who do not want to get their hands dirty.

The code for RoninDojo is open-source, so it is also possible to install this solution on your own hardware. This option is cost-effective but requires a bit more manipulation, which is what we will do in this article.

RoninDojo is a Dojo, so it allows you to easily integrate Whirlpool CLI into your Bitcoin node to have the best possible CoinJoin experience. With Whirlpool CLI, not only can you let your bitcoins remix 24/7 without needing to keep your personal computer on, but you can also greatly improve your privacy.

RoninDojo integrates many other tools that rely on your Dojo, such as the Boltzmann calculator, which determines the degree of transaction privacy, the Electrum server to connect your different Bitcoin wallets to your node, or the Mempool server to privately observe your transactions.
Par rapport à une autre solution de nœud comme Umbrel, que je vous ai présentée dans cet article, RoninDojo s'inscrit dans une ligne de développement profondément tournée vers les solutions "On Chain" et vers des outils permettant d'optimiser la confidentialité des utilisateurs. RoninDojo ne permet donc pas d'interagir avec le Lightning Network.

Un RoninDojo propose moins d'outils par rapport à un Umbrel, mais les quelques fonctionnalités essentielles pour un Bitcoiner présentes sur Ronin sont incroyablement stables.

Donc si vous n'avez pas besoin de toutes les fonctionnalités d'un serveur Umbrel, et que vous souhaitez exclusivement disposer d'un nœud simple et stable avec quelques outils essentiels comme Whirlpool ou Mempool, alors RoninDojo est sûrement une bonne solution pour vous.

Selon moi, la ligne de développement d'Umbrel est très tournée vers le Lightning Network et vers des outils polyvalents. Cela reste un nœud Bitcoin, mais on cherche à en faire un mini-serveur multi-tâches. À l'inverse, la ligne de développement de RoninDojo se rapproche plus de celle des équipes de Samourai Wallet, et se focalise sur les outils essentiels d'un Bitcoiner lui permettant une pleine indépendance et un gestion optimisée de sa confidentialité sur Bitcoin.

Veuillez noter que la mise en place d'un nœud RoninDojo reste légèrement plus complexe qu'un nœud Umbrel.

Maintenant que nous avons pu dresser le portrait de RoninDojo, voyons ensemble comment mettre en place ce nœud.

## Quel matériel choisir ?

Pour choisir la machine qui héberge et fait tourner RoninDojo, vous disposez de plusieurs options.

Comme expliqué précédemment, le choix le plus simple sera de commander le Tanto, une machine plug-and-play conçue spécialement pour cet usage. Pour commander le votre, c'est par ici : [lien vers le Tanto](https://shop.ronindojo.io/product-category/nodes/).

Etant donné que les équipes de RoninDojo produisent du code open-source, il est également possible d'implémenter RoninDojo sur d'autres machines. Vous pouvez ainsi retrouver les dernières versions de l'assistant d'installation sur cette page : [lien vers l'assistant d'installation](https://ronindojo.io/en/downloads.html), et les dernières versions du code sur cette page : [lien vers les dernières versions du code](https://code.samourai.io/ronindojo/RoninDojo).

Personnellement, je l'ai installé sur un Raspberry Pi 4 8GO et tout fonctionne parfaitement.

Attention tout de même, les équipes de RoninDojo nous indiquent qu'il y a souvent des problèmes à cause du boitier et de l'adaptateur du SSD. Il est donc déconseillé d'utiliser un boitier avec un câble pour le SSD de votre machine. Préférez plutôt utiliser une carte d'extension de stockage spécialement conçue pour votre carte mère comme celle-ci : [Carte d'extension de stockage Raspberry Pi 4](lien vers la carte d'extension de stockage).

Voici un exemple de mise en place pour faire votre propre nœud RoninDojo :

- Un Raspberry Pi 4.
- Un boitier avec un ventilateur.
- Una scheda di espansione di archiviazione compatibile.
- Un cavo di alimentazione.
- Una micro SD industriale da 16GB o più.
- Un SSD da 1TB o più.
- Un cavo ethernet RJ45, consigliata categoria 8.

## Come installare RoninDojo?

### Passaggio 1: Preparare la micro SD avviabile.

Una volta che hai assemblato la tua macchina, puoi iniziare l'installazione di RoninDojo. Per farlo, inizia creando una micro SD avviabile scrivendo l'immagine disco corretta.

Inserisci la tua scheda micro SD nel tuo computer personale, quindi vai al sito ufficiale di RoninDojo per scaricare l'immagine disco di RoninOS: https://ronindojo.io/en/downloads.html.

Scarica l'immagine disco corrispondente al tuo hardware. Nel mio caso, ho scaricato l'immagine "MANJARO-ARM-RONINOS-RPI4-22.03.IMG.XZ":

![Scarica l'immagine disco di RoninOS](assets/2.png)

Una volta scaricata l'immagine, verifica la sua integrità utilizzando il file .SHA256 corrispondente. Spiego dettagliatamente come fare questo in questo articolo: Come verificare l'integrità di un software Bitcoin su Windows?

Le istruzioni specifiche per verificare l'integrità di RoninOS sono disponibili anche in questa pagina in inglese: https://wiki.ronindojo.io/en/extras/verify.

Per scrivere questa immagine sulla tua micro SD, puoi utilizzare un software come Balena Etcher che puoi scaricare qui: https://www.balena.io/etcher/.

Per farlo, seleziona l'immagine in Etcher e scrivila sulla micro SD:

![Scrivi l'immagine disco con Etcher](assets/3.png)

Una volta completata l'operazione, puoi inserire la micro SD avviabile nel Raspberry Pi e accendere la macchina.

### Passaggio 2: Configurare RoninOS.

RoninOS è il sistema operativo del tuo nodo RoninDojo, è una versione modificata di Manjaro, una distribuzione Linux. Dopo aver avviato la tua macchina e aspettato alcuni minuti, puoi iniziare la configurazione.

Per connetterti in remoto, devi trovare l'indirizzo IP della tua macchina RoninDojo. Puoi farlo ad esempio accedendo al pannello di amministrazione del tuo router, oppure puoi anche scaricare un software come https://angryip.org/ per scansionare la tua rete locale e trovare l'IP della macchina.

Una volta trovato l'IP, puoi prendere il controllo della tua macchina da un altro computer connesso alla stessa rete locale utilizzando SSH.

Da un computer con MacOS o Linux, apri semplicemente il terminale. Da un computer con Windows, puoi utilizzare uno strumento specializzato come Putty o direttamente Windows PowerShell.

Una volta aperto il terminale, digita il seguente comando:

> ssh root@192.168.?.?

Sostituisci semplicemente i due punti interrogativi con l'IP del tuo RoninDojo trovato in precedenza.

> Suggerimento: In una shell, fai clic destro per incollare un elemento.

Successivamente, arriverai alla schermata di configurazione di Manjaro. Scegli la giusta disposizione della tastiera utilizzando le frecce per cambiare destinazione nella lista a discesa.

![Configurazione della tastiera Manjaro](assets/4.png)

Scegli un nome utente e una password per la tua sessione. Utilizza una password forte e fai un backup sicuro. Puoi eventualmente utilizzare una password leggera durante l'installazione e successivamente modificare facilmente questa password con la possibilità di "copia e incolla" in RoninUI. Questo ti permetterà di impostare una password molto robusta senza doverla scrivere manualmente durante l'installazione di Manjaro.

![Configurazione del nome utente Manjaro](assets/5.png)

Successivamente, ti verrà chiesto di scegliere una password root. Per la password root, inserisci direttamente una password forte. Non avrai la possibilità di modificarla da RoninUI. Ricorda anche di fare un backup sicuro di questa password root.

Successivamente, inserisci la tua località e la tua zona oraria.

![Configurazione della zona oraria Manjaro](assets/6.png)

![Configurazione della località Manjaro](assets/7.png)

Successivamente, scegli un nome host.

![Configurazione del nome host Manjaro](assets/8.png)

Infine, verifica le informazioni di configurazione di Manjaro e conferma.

![Verifica delle informazioni di configurazione di ManjaroOS](assets/9.png)

### Passaggio 3: Scarica RoninDojo.

La configurazione iniziale di RoninOS verrà eseguita. Una volta completata come mostrato nella schermata sopra, la macchina si riavvierà. Attendi quindi qualche istante, quindi inserisci il seguente comando per connetterti nuovamente alla tua macchina RoninDojo:

> ssh pseudo@192.168.?.?

Sostituisci semplicemente "pseudo" con il nome utente che hai scelto in precedenza e sostituisci i punti interrogativi con l'IP del tuo RoninDojo.

Successivamente, inserisci la tua password utente.

Nel terminale, apparirà così:

![Connessione SSH a RoninOS](assets/10.png)

Ora sei connesso alla tua macchina che al momento dispone solo di RoninOS. Ora dovrai installare RoninDojo.

Scarica l'ultima versione di RoninDojo inserendo il seguente comando:

> git clone https://code.samourai.io/ronindojo/RoninDojo

Il download verrà eseguito rapidamente. Nel terminale apparirà così:

![Clonazione di RoninDojo](assets/11.png)

Attendi il completamento del download, quindi installa e accedi all'interfaccia utente di RoninDojo utilizzando il seguente comando:

> ~/RoninDojo/ronin

Ti verrà quindi chiesto di inserire la tua password utente:

![Verifica password del nodo Bitcoin](assets/12.png)'

> Questo comando è necessario solo la prima volta che accedi al tuo RoninDojo. Successivamente, per accedere a RoninCLI tramite SSH, dovrai semplicemente inserire il comando [SSH pseudo@192.168.?.?] sostituendo "pseudo" con il tuo nome utente e inserendo l'IP del tuo nodo. Ti verrà richiesta la password dell'utente.

Successivamente vedrai questa bellissima animazione:

![Animazione di avvio di RoninCLI](assets/13.png)

Poi finalmente arriverai all'interfaccia utente CLI di RoninDojo.

### Passaggio 4: Installare RoninDojo.

Dal menu principale, accedi al menu "System" utilizzando le frecce della tastiera. Utilizza il tasto Invio per confermare la tua scelta.

![Navigazione menu RoninCLI verso System](assets/14.png)

Quindi vai al menu "System Setup & Install".

![Navigazione menu RoninCLI verso installazione sistema RoninDojo](assets/15.png)

Infine, seleziona "System Setup" e "Install RoninDojo" utilizzando la barra spaziatrice, quindi seleziona "Accetta" per avviare l'installazione.

![Conferma installazione RoninDojo](assets/16.png)

Lascia che l'installazione si completi tranquillamente. Nel mio caso ci sono volute circa 2 ore. Mantieni aperto il tuo terminale durante l'operazione.

Osserva occasionalmente il tuo terminale, ti verrà chiesto di premere un tasto in determinati momenti dell'installazione, come ad esempio qui:

![Installazione di RoninDojo in corso](assets/17.png)

Alla fine dell'installazione, vedrai i diversi container avviarsi:

![Avvio dei container del nodo](assets/18.png)

Poi il tuo nodo si riavvierà. Riconnettiti a RoninCLI per il passaggio successivo.

![Riavvio del nodo Bitcoin](assets/19.png)

### Passaggio 5: Scaricare la catena di proof of work e accedere a RoninUI.

Una volta completata l'installazione, il tuo nodo inizierà a scaricare la catena di proof of work di Bitcoin. Questo è ciò che viene chiamato IBD (Initial Block Download). Di solito ci vogliono tra 2 e 14 giorni a seconda della tua connessione internet e del tuo dispositivo.

Puoi seguire l'avanzamento del download della catena accedendo all'interfaccia web di RoninUI.

Per accedervi da una rete locale, digita sul tuo browser nella barra degli indirizzi:

- O direttamente l'indirizzo IP della tua macchina (192.168.?.?)

- O: ronindojo.local

Ricorda di disattivare il tuo VPN se ne stai usando uno.

### Possibile complicazione

Se non riesci a connetterti a RoninUI dal tuo browser, verifica il corretto funzionamento dell'applicazione dal tuo Terminale connesso al tuo nodo tramite SSH. Accedi al menu principale seguendo le istruzioni precedenti:

- Digita: SSH pseudo@192.168.?.? sostituendo con le tue credenziali.

- Inserisci la tua password utente.
  Une volta nel menu principale, vai su:
  > RoninUI > Riavvia

Se l'applicazione si riavvia correttamente, il problema è a livello di connessione dal tuo browser. Verifica di non utilizzare una VPN e assicurati di essere connesso alla stessa rete del tuo nodo.

Se il riavvio restituisce un errore, prova ad aggiornare il sistema operativo e reinstalla RoninUI. Per aggiornare il sistema operativo:

> Sistema > Aggiornamenti software > Aggiorna sistema operativo

Una volta completato l'aggiornamento e il riavvio, ricollegati al tuo nodo tramite SSH e reinstalla RoninUI:

> RoninUI > Reinstalla

Dopo aver scaricato nuovamente RoninUI, prova a connetterti tramite il tuo browser a RoninUI.

> Suggerimento: Se esci da RoninCLI per errore e ti ritrovi sul terminale Manjaro, digita semplicemente il comando "ronin" per tornare direttamente al menu principale di RoninCLI.

### Accesso web

Puoi anche accedere all'interfaccia web di RoninUI da qualsiasi rete utilizzando Tor. Per farlo, ottieni l'indirizzo Tor di RoninUI da RoninCLI:

> Credenziali > Ronin UI

Prendi l'indirizzo Tor che termina con .onion e accedi a Ronin UI inserendo questo indirizzo nel tuo browser Tor. Attenzione a non divulgare le tue credenziali, sono informazioni sensibili.

![Interfaccia web di accesso a RoninUI](assets/20.png)

Una volta connesso, ti verrà richiesta la password dell'utente. È la stessa che usi per connetterti tramite SSH.

![Pannello di gestione di RoninUI interfaccia web](assets/21.png)

Possiamo osservare l'avanzamento dell'IBD. Sii paziente, stai recuperando tutte le transazioni effettuate su Bitcoin dal 3 gennaio 2009.

Dopo aver scaricato l'intera blockchain, l'indicizzatore compatterà il database. Questa operazione richiede circa 12 ore. Puoi anche seguire il suo progresso su "Indicizzatore" su RoninUI.

Il tuo nodo RoninDojo sarà completamente funzionale dopo questo:

![Indicizzatore sincronizzato al 100% nodo funzionale](assets/22.png)

Se desideri cambiare la password dell'utente per renderla più sicura, puoi farlo ora dall'opzione "Impostazioni". Su RoninDojo, non c'è uno strato di sicurezza aggiuntivo, quindi ti consiglio di scegliere una password veramente robusta e di fare una copia di backup adeguata.

## Come utilizzare RoninDojo?

Una volta che la blockchain è stata scaricata e compattata, puoi iniziare a utilizzare i servizi offerti dal tuo nuovo nodo RoninDojo. Vediamo insieme come utilizzarli.

### Collegare i tuoi portafogli software a electrs.

La prima utilità del tuo nodo appena installato e sincronizzato sarà quella di diffondere le tue transazioni alla rete Bitcoin. Quindi probabilmente vorrai connettere i tuoi diversi software di gestione dei portafogli.

Puoi farlo tramite Electrum Rust Server (electrs). L'applicazione è normalmente preinstallata sul tuo nodo RoninDojo. Se non è così, puoi installarla manualmente dall'interfaccia RoninCLI.

Basta andare su:

> Applicazioni > Gestisci applicazioni > Installa Electrum Server

Per ottenere l'indirizzo Tor del tuo Electrum Server, dal menu RoninCLI, vai su:

> Credenziali > Electrs

Dovrai semplicemente inserire il link in .onion nel software del tuo portafoglio. Ad esempio, su Sparrow Wallet, basta andare nella scheda:

> File > Preferenze > Server

Nel tipo di server, seleziona "Private Electrum", quindi inserisci l'indirizzo Tor del tuo Server Electrum nel campo corrispondente. Infine, clicca su "Test Connection" per testare e salvare la tua connessione.

![Interfaccia di connessione di Sparrow Wallet a un electrs](assets/23.png)

### Collegare i software dei portafogli a Samourai Dojo.

Invece di utilizzare Electrs, puoi anche utilizzare Samourai Dojo per collegare il tuo portafoglio software compatibile al tuo nodo RoninDojo. Ad esempio, Samourai Wallet offre questa opzione.

Per farlo, sarà sufficiente scannerizzare il codice QR di connessione del tuo Dojo. Per accedervi da RoninUI, clicca sulla scheda "Dashboard" e poi sul pulsante "Gestisci" nella casella del tuo Dojo. Potrai quindi vedere i codici QR di connessione al tuo Dojo e a BTC-RPC Explorer. Per visualizzarli in chiaro, clicca su "Mostra valori".

![Recupero del codice QR di connessione al Dojo](assets/24.png)

Per collegare il tuo portafoglio Samourai Wallet al tuo Dojo, dovrai scannerizzare questo codice QR durante l'installazione dell'applicazione:

![Connessione a Dojo dall'applicazione Samourai Wallet](assets/25.png)

### Utilizzare il proprio Explorer Mempool.

Strumento essenziale per i Bitcoiner, l'explorer ti permette di verificare diverse informazioni sulla catena Bitcoin. Con Mempool, ad esempio, puoi verificare in tempo reale le commissioni applicate dagli altri utenti per regolare al meglio le tue. Puoi anche verificare lo stato di conferma di una delle tue transazioni, o guardare il saldo di un indirizzo.

Questi strumenti di explorer possono esporre a rischi di perdita di privacy e ti obbligano a fidarti del database di un terzo. Quando utilizzi questo strumento online senza passare per il tuo proprio nodo:

- Rischierai di divulgare informazioni sul tuo portafoglio.

- Ti affidi al gestore del sito web per la catena di proof of work che ospita.
  Al fine di evitare questi rischi, è possibile utilizzare la propria istanza Mempool sul proprio nodo tramite la rete Tor. Con questa soluzione, non solo si preserva la propria privacy durante l'utilizzo del servizio, ma non è più necessario fidarsi di un provider poiché si interroga il proprio database.

Per fare ciò, inizia installando Mempool Space Visualizer da RoninCLI:

> Applicazioni > Gestisci applicazioni > Installa Mempool Space Visualizer

Una volta installato, recupera il link per la tua Mempool. L'indirizzo Tor ti permetterà di accedervi da qualsiasi rete. Allo stesso modo, recuperiamo questo link tramite RoninCLI:

> Credenziali > Mempool

![Recupero indirizzo Tor Mempool](assets/26.png)

Inserisci semplicemente il tuo indirizzo Mempool Tor nel browser Tor per usufruire della propria istanza Mempool, basata sui propri dati. Consiglio di aggiungere questo indirizzo Tor ai preferiti per potervi accedere più rapidamente. Puoi anche crearne un collegamento sul desktop.

![Interfaccia Mempool Space](assets/27.png)

Se non hai ancora il browser Tor, puoi scaricarlo qui: https://www.torproject.org/download/

Puoi anche accedervi dal tuo smartphone installando Tor Browser e inserendo lo stesso indirizzo. Da qualsiasi luogo, potrai monitorare lo stato della catena Bitcoin utilizzando il proprio nodo.

### Utilizzare Whirlpool CLI.

Il tuo nodo RoninDojo include anche WhirlpoolCLI, un'interfaccia a linea di comando remota per automatizzare i mix Whirlpool.

Quando si effettua un CoinJoin con l'implementazione Whirlpool, l'applicazione utilizzata deve rimanere aperta per eseguire mix e remix. Questo processo può essere tedioso per l'utente che desidera avere anon sets elevati, poiché il dispositivo che ospita l'applicazione con Whirlpool deve rimanere costantemente acceso. In pratica, ciò significa che se si desidera impegnare i propri UTXO in remix 24 ore su 24, sarà necessario lasciare il proprio computer personale o telefono acceso con l'applicazione aperta.

Una soluzione a questa limitazione è utilizzare WhirlpoolCLI su una macchina destinata a rimanere costantemente accesa, come ad esempio un nodo Bitcoin. Grazie a questo, i nostri UTXO potranno essere remixati 24 ore su 24 e 7 giorni su 7 senza dover lasciare un'altra macchina oltre al nostro nodo Bitcoin in funzione.
'WhirlpoolCLI s'utilizza con WhirlpoolGUI, un'interfaccia grafica da installare su un computer personale che consente di gestire facilmente i Coinjoin. Vi spiegherò in dettaglio come configurare Whirlpool CLI con il vostro dojo personale in questo articolo: [link](https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin#:~:text=dans%20cette%20partie.-,Tutoriel%20%3A%20Whirpool%20CLI%20sur%20Dojo%20et%20Whirlpool%20GUI.,-Si%20vous%20souhaitez)

Per saperne di più sul Coinjoin in generale, vi spiego tutto in questo articolo: [link](https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin)

### Utilizzare Whirlpool Stat Tool.

Dopo aver eseguito CoinJoin con Whirlpool, potreste voler sapere concretamente quale è il livello di privacy delle vostre UTXO mixate. Whirlpool Stat Tool vi permette di fare questo facilmente. Grazie a questo strumento, potrete calcolare il punteggio prospettico e il punteggio retrospettivo delle vostre UTXO mixate. Per saperne di più sul calcolo di questi Anon Sets e sul loro funzionamento, vi consiglio di leggere questa parte: [link](https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin#:~:text=perdre%20en%20confidentialit%C3%A9.-,Anon%20Sets.,-Comme%20expliqu%C3%A9%20pr%C3%A9c%C3%A9demment)

Lo strumento è preinstallato sul vostro RoninDojo. Al momento, è disponibile solo da RoninCLI. Per avviarlo dal menu principale, andate su:

> Samourai Toolkit > Whirlpool Stat Tool

Le istruzioni per l'uso verranno visualizzate. Una volta completato, premere qualsiasi tasto per accedere alle righe di comando:

![Accueil logiciel Whirlpool Stats Tool](assets/28.png)

Verrà visualizzato il terminale:

> wst#/tmp>

Per uscire da questa interfaccia e tornare al menu RoninCLI, digitare semplicemente il comando:

> quit

Per iniziare, impostiamo il proxy su Tor per estrarre i dati da OXT in modo confidenziale. Digitare il comando:

> socks5 127.0.0.1:9050

Successivamente, scaricare i dati del pool che contiene la vostra transazione:

> download 0001
>
> Sostituire 0001 con il codice di denominazione del pool di interesse.

I codici di denominazione sono i seguenti su WST:

- Pool 0,5 bitcoin: 05

- Pool 0,05 bitcoin: 005

- Pool 0,01 bitcoin: 001

- Pool 0,001 bitcoin: 0001

![Téléchargement des données de la pool 0001 depuis OXT](assets/29.png)

Una volta scaricati i dati, caricarli con il comando:

> load 0001
>
> Sostituire 0001 con il codice di denominazione del pool di interesse.'
> ![Loading data from pool 0001](assets/30.png)
> Lascia che il caricamento avvenga, potrebbe richiedere alcuni minuti. Dopo aver caricato i dati, digita il comando score seguito dal tuo TXID (identificativo della transazione) per ottenere i suoi Anon Sets:

> score TXID
>
> Sostituisci TXID con l'identificativo della tua transazione.

![Stampa dei punteggi prospettici e retrospettivi del TXID fornito](assets/31.png)

WST ti mostrerà quindi il punteggio retrospettivo (Backward-looking metrics) e poi il punteggio prospettico (Forward-looking metrics). Oltre ai punteggi degli Anon Sets, WST ti fornisce anche il tasso di diffusione del tuo output nel pool in base all'anon set.

Si prega di notare che il punteggio prospettico del tuo UTXO viene calcolato a partire dal TXID del tuo mix iniziale, non dal tuo ultimo mix. Al contrario, il punteggio retrospettivo di un UTXO viene calcolato a partire dal TXID dell'ultimo ciclo.

Ancora una volta, se non comprendi questi concetti degli Anon Sets, ti consiglio di leggere questa parte del mio articolo su Coinjoin in cui spiego tutto in dettaglio con schemi: [https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin#:~:text=perdre%20en%20confidentialit%C3%A9.-,Anon%20Sets.,-Comme%20expliqu%C3%A9%20pr%C3%A9c%C3%A9demment](https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin#:~:text=perdre%20en%20confidentialit%C3%A9.-,Anon%20Sets.,-Comme%20expliqu%C3%A9%20pr%C3%A9c%C3%A9demment)

### Utilizzare il calcolatore Boltzmann.

Il calcolatore Boltzmann è uno strumento che ti permette di calcolare facilmente diverse metriche avanzate su una transazione Bitcoin, inclusi il suo livello di entropia. Tutti questi dati ti permetteranno di attribuire dei numeri al livello di privacy di una transazione e di individuare eventuali errori. Questo strumento è preinstallato nel tuo nodo RoninDojo.

Per accedervi da RoninCLI, connettiti tramite SSH e vai al menu:

> Samourai Toolkit > Boltzmann Calculator

Prima di spiegarti come utilizzarlo su RoninDojo, ti spiegherò cosa rappresentano queste metriche, come vengono calcolate e a cosa servono.

Questi indicatori possono essere utilizzati per qualsiasi transazione Bitcoin, ma sono particolarmente interessanti per studiare la qualità di una transazione Coinjoin.

1. Il primo indicatore calcolato da questo software è il numero di combinazioni possibili. Viene indicato nel calcolatore come "nb combinations". Considerando i valori degli UTXO, questo indicatore rappresenta il numero di mappature possibili delle voci verso le uscite.

> Se non ti senti a tuo agio con il termine "UTXO", ti consiglio di leggere questo breve articolo: Meccanismo di una transazione Bitcoin: UTXO, input e output.
> In altre parole, questo indicatore rappresenta il numero di interpretazioni possibili per una transazione data. Ad esempio: una struttura Coinjoin Whirlpool 5x5 avrà un numero di combinazioni possibili pari a 1496:
> ![Schema di una transazione Coinjoin su kycp.org](assets/32.png)

Crediti: https://kycp.org/#/fe5e5abab7ea452f87603f7ebc2fa4e77380eafcc927e1cb51e1a72401ab073d

2. Il secondo indicatore calcolato è l'entropia di una transazione ("Entropy"). Dato che il numero di combinazioni possibili può essere molto elevato per una transazione, si può scegliere di utilizzare l'entropia. L'entropia rappresenta il logaritmo binario del numero di combinazioni possibili. La sua formula è la seguente:

- E: entropia della transazione.

- C: numero di combinazioni possibili per la transazione.

> E = log2(C)

In matematica, il logaritmo binario (base 2) è la funzione inversa della funzione potenza di 2. In altre parole, il logaritmo binario di x è la potenza a cui il numero 2 deve essere elevato per ottenere il valore x.

Quindi:

> E = log2(C)
> C = 2^E

Questo indicatore è quindi espresso in bit. Ad esempio, ecco il calcolo dell'entropia di una transazione Coinjoin con struttura Whirlpool 5x5, con un numero di combinazioni possibili pari a 1496:

> C = 1496
>
> E = log2(1496)
>
> E = 10.5469 bit

Questa transazione Coinjoin ha quindi un'entropia di 10.5469 bit, il che è molto buono.

Più alto è questo indicatore, più ci sono interpretazioni diverse della transazione e quindi maggiore è la sua confidenzialità.

Prendiamo un altro esempio. Ecco una transazione "classica" che ha un input e due output:

![Schema di transazione bitcoin su oxt.me](assets/34.png)

Crediti: https://oxt.me/graph/transaction/tiid/9815286

Questa transazione ha solo un'interpretazione possibile:

> [(inp 0) > (Outp 0 ; Outp 1)]

Quindi la sua entropia sarà uguale a 0:

> C = 1
>
> E = log2(C)
>
> E = 0

3. Il terzo indicatore restituito dal calcolatore Boltzmann è l'efficienza del portafoglio della Tx chiamata "Wallet Efficiency". Questo indicatore permette semplicemente di confrontare la transazione in ingresso con la migliore transazione possibile nella stessa configurazione.
   Si introdurrà quindi il concetto di entropia massima che rappresenta l'entropia più alta raggiungibile per una struttura di transazione data. Ad esempio, la struttura di Coinjoin di tipo Whirlpool 5x5 avrà un'entropia massima pari a 10.5469. L'indicatore di efficienza confronta quindi questa entropia massima con l'entropia effettiva della transazione in ingresso. La sua formula è la seguente per:

- ER: Entropia effettiva espressa in bit.
- EM: Entropia massima con la stessa struttura espressa in bit.
- Ef: Efficienza espressa in bit.

> Ef = ER - EM
>
> Ef = 10.5469 - 10.5469
>
> Ef = 0 bit

Questo indicatore è anche espresso in percentuale, quindi la sua formula diventa:

- CR: Numero di combinazioni possibili effettive.
- CM: Numero di combinazioni possibili al massimo con la stessa struttura.
- Ef: Efficienza espressa in percentuale.

> Ef = CR/CM
>
> Ef = 1496/1496
>
> Ef = 100%

Un'efficienza del 100% significa quindi che questa transazione ha il massimo livello di privacy possibile rispetto alla sua struttura.

4. Il quarto indicatore calcolato è la densità dell'entropia ("Entropy Density"). Permette di rapportare l'entropia a ciascun input o output. Pertanto, questo indicatore può essere utilizzato per confrontare l'efficienza tra diverse transazioni di dimensioni diverse.

Il calcolo è molto semplice, si divide l'entropia della transazione per il numero di input e output presenti. Ad esempio, per un Coinjoin di tipo Whirlpool 5x5 avremo:

    ED: Densità dell'entropia espressa in bit.
    E: Entropia della transazione espressa in bit.
    T: numero totale di input e output nella transazione.

T = 5 + 5 = 10
ED = E / T
ED = 10.5469 / 10
ED = 1.054 bit

La quinta informazione fornita dal calcolatore Boltzmann è la tabella delle probabilità di collegamento tra input e output. Questa tabella fornirà semplicemente la probabilità (punteggio di Boltzmann) che un determinato input corrisponda a un determinato output.

Se riprendiamo il nostro esempio con un Coinjoin Whirlpool, la tabella delle probabilità sarà:

| Input | Output 0 | Output 1 | Output 2 | Output 3 | Output 4 |
| ----- | -------- | -------- | -------- | -------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0     | 34%      | 34%      | 34%      | 34%      | 34%      |
| 1     | 34%      | 34%      | 34%      | 34%      | 34%      |
| 2     | 34%      | 34%      | 34%      | 34%      | 34%      |
| '     | 3        | 34%      | 34%      | 34%      | 34%      | 34% |     | 4   | 34% | 34% | 34% | 34% | 34% |

Si può vedere qui che ogni input ha la stessa probabilità di essere collegato a ogni output.

Tuttavia, se prendiamo ad esempio una transazione con un input e due output, allora avremo:

| Input | Output 0 | Output 1 |
| ----- | -------- | -------- |
| 0     | 100%     | 100%     |

In questo esempio possiamo vedere che la probabilità che ogni output provenga dall'input 0 è del 100%.

Più bassa è questa probabilità, maggiore sarà la privacy.

6. La sesta informazione calcolata è il numero di collegamenti deterministici. Vi verrà anche fornito il rapporto dei collegamenti deterministici. Questo indicatore mette in evidenza il numero di collegamenti tra gli input e gli output della transazione che hanno una probabilità del 100%, cioè sono indiscutibili.

Il rapporto indica quindi il numero di collegamenti deterministici nella transazione rispetto al numero totale di collegamenti.

Ad esempio, una transazione Coinjoin Whirlpool non ha alcun collegamento deterministico tra gli input e gli output. L'indicatore sarà quindi uguale a zero e il rapporto sarà anche del 0%.

Tuttavia, per la seconda transazione studiata (1 input e 2 output), l'indicatore è uguale a 2 e il rapporto è del 100%.

Quindi se questo indicatore è uguale a zero, indica una buona privacy.

Ora che abbiamo studiato gli indicatori, vediamo come calcolarli utilizzando questo software. Da RoninCLI, vai al menu:

> Samourai Toolkit > Boltzmann Calculator

![Accueil du logiciel Boltzmann Calculator](assets/35.png)

Una volta avviato il software, inserisci l'ID della transazione che desideri studiare. Puoi inserire più transazioni separandole con una virgola, quindi premi Invio:

![Taper une TXID à étudier sur Boltzmann Calculator](assets/36.png)

Il calcolatore restituirà tutti gli indicatori che abbiamo visto in precedenza:

![Impression des données de Boltzmann Calculator pour cette TXID](assets/37.png)

Digita il comando "Quit" per uscire dal software e tornare al menu di RoninCLI.

Per saperne di più sul calcolatore Boltzmann, ti consiglio di leggere questi articoli:

- https://medium.com/@laurentmt/introducing-boltzmann-85930984a159

- https://gist.github.com/LaurentMT/e758767ca4038ac40aaf

### Collegare Bisq.

Bisq è una piattaforma di scambio che consente di acquistare e vendere bitcoin peer-to-peer. Viene utilizzato con un software desktop che viene eseguito su Tor e consente di scambiare bitcoin senza dover fornire la propria identità.'
Bisq sicurezza gli scambi peer-to-peer grazie a un sistema di multi-firma 2/2. Puoi utilizzare questo software con il tuo nodo RoninDojo per ottimizzare la privacy delle tue transazioni e fidarti dei dati della blockchain del tuo nodo.

Per scaricare il software Bisq, vai al loro sito ufficiale: https://bisq.network/

Per familiarizzare con il software, ti consiglio di leggere questa pagina: https://bisq.network/getting-started/

Per ottenere il link di connessione dal tuo RoninDojo, dovrai connetterti a RoninCLI tramite SSH. Quindi vai al menu:

> Applicazioni > Gestisci applicazioni

Inserisci la tua password e spunta la casella con il tasto spazio:

> [ ] Abilita connessione Bisq

Conferma la tua scelta. Lascia che il tuo nodo si installi, quindi vai a recuperare l'indirizzo Tor V3 da:

> Credenziali > Bitcoind

Copia l'indirizzo sotto "Bitcoin Daemon".

Puoi anche recuperare il tuo indirizzo Bitcoind Tor V3 dall'interfaccia RoninUI semplicemente cliccando su "Gestisci" nella sezione "Bitcoin Core" dal "Dashboard":

![Recupera indirizzo TorV3 Bitcoin Daemon su RoninUI](assets/38.png)

Per connettere il tuo nodo a Bisq, vai al menu:

> Impostazioni > Informazioni sulla rete

![Accedi all'interfaccia di connessione al nodo dal software Bisq](assets/39.png)

Clicca sulla bolla "Utilizza nodi Bitcoin Core personalizzati". Quindi inserisci il tuo indirizzo Bitcoin TorV3 nella casella apposita, con ".onion" ma senza "http://".

![Casella per inserire l'indirizzo TorV3 del tuo nodo nel software Bisq](assets/40.png)

Riavvia il software Bisq. Il tuo nodo è ora connesso al tuo Bisq.

### Altre funzionalità.

Il tuo nodo RoninDojo include anche altre funzionalità di base. Hai la possibilità di scansionare informazioni specifiche per assicurarti che vengano prese in considerazione.

Ad esempio, potrebbe capitare che il tuo portafoglio collegato al tuo RoninDojo non trovi i bitcoin che ti appartengono. Il saldo è a 0 anche se sei sicuro di possedere bitcoin in quel portafoglio. Ci sono molte possibili cause da considerare, tra cui un errore nei percorsi di derivazione, e tra queste è anche possibile che il tuo nodo non stia osservando i tuoi indirizzi.

Per risolvere il problema, puoi verificare che il tuo nodo stia tracciando correttamente il tuo xpub con lo strumento "xpub tool". Per accedere a questo strumento da RoninUI, vai al menu:

> Manutenzione > Strumento XPUB

Inserisci l'xpub che sta causando il problema e clicca su "Verifica" per controllare queste informazioni.

![Strumento XPUB da RoninUI](assets/41.png)

Se il tuo xpub viene tracciato correttamente dal nodo, vedrai apparire questo:

![Risultato positivo dell'analisi dello strumento XPUB](assets/42.png)
Verifica che tutte le transazioni siano correttamente visualizzate. Verifica anche che il tipo di derivazione corrisponda a quello del tuo portafoglio. Qui possiamo vedere che il nodo interpreta questo xpub come una derivazione BIP44. Se questo tipo di derivazione non corrisponde a quello del tuo portafoglio, clicca sul pulsante "Retype", quindi seleziona BIP44/BIP49/BIP84 in base alla tua scelta:
![Changer le type de dérivation de la xpub étudiée depuis RoninUI](assets/43.png)

Se il tuo xpub non è tracciato dal tuo nodo, vedrai comparire questa schermata che ti invita ad importarlo:
![Importer une xpub avec outil XPUB Tool sur RoninUI](assets/44.png)

Puoi anche utilizzare altri strumenti di manutenzione:

- Transaction Tool: ti consente di osservare i dettagli di una transazione specifica.
- Address Tool: ti consente di verificare se un indirizzo specifico è tracciato correttamente dal tuo Dojo.
- Rescan Blocks: forza il tuo nodo a scansionare nuovamente un intervallo di blocchi selezionato.

Troverai anche sull'interfaccia di RoninUI lo strumento "Push Tx". Ti consente di diffondere una transazione firmata sulla rete Bitcoin. Questa deve essere inserita nel formato esadecimale:
![Outil de diffusion d'une transaction signée depuis RoninUI](assets/45.png)

## Conclusion.

Abbiamo potuto vedere come installare e utilizzare questo magnifico strumento che è RoninDojo. È una scelta eccellente per eseguire il proprio nodo Bitcoin. È una soluzione stabile che integra e tiene aggiornati tutti gli strumenti essenziali per un Bitcoiner.

Se l'uso del terminale non ti spaventa e se non hai bisogno di strumenti legati alla Lightning Network, allora RoninDojo potrebbe piacerti.

Se puoi, considera di fare una donazione agli sviluppatori che producono gratuitamente questi software liberi e open source per te: https://donate.ronindojo.io/

Per saperne di più su RoninDojo, ti consiglio di consultare i link nelle mie risorse esterne di seguito.

### Per approfondire:

- Comprendere e utilizzare il CoinJoin su Bitcoin.
- Le funzioni di hash - estratto dall'ebook Bitcoin Démocratisé 1.
- Tutto quello che c'è da sapere sulla Passphrase Bitcoin.

### Risorse esterne:

- https://samouraiwallet.com/dojo
- https://ronindojo.io/index.html
- https://wiki.ronindojo.io/en/home
- https://code.samourai.io/ronindojo/RoninDojo
- https://gist.github.com/LaurentMT/e758767ca4038ac40aaf
- https://medium.com/@laurentmt/introducing-boltzmann-85930984a159
- https://oxt.me/
- https://kycp.org/#/
- https://fr.wikipedia.org/wiki/Formule_de_Boltzmann
- https://wiki.ronindojo.io/en/setup/bisq
- https://bisq.network/

https://www.pandul.fr/post/installer-et-utiliser-son-n%C5%93ud-bitcoin-ronindojo
