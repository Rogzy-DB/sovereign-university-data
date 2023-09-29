---
name: GrapheneOS

description: Tutorial di Graphene OS
---

# Graphene OS

> "[GrapheneOS](https://grapheneos.org/) è un sistema operativo mobile focalizzato sulla privacy e la sicurezza, con compatibilità delle app Android, sviluppato come progetto open source senza scopo di lucro."

GrapheneOS, originariamente fondato nel 2014 come 'CopperheadOS', si basa sul tradizionale codice Android (AOSP), ma con molte modifiche e miglioramenti mirati a migliorare la privacy e la sicurezza dell'utente. GrapheneOS mette l'utente al controllo del proprio telefono, non delle grandi aziende tecnologiche.

### Sommario:

- Introduzione
- Preparazione
- Installazione
- Alternative alle app
- Svantaggi
- Informazioni utili

Guida di https://github.com/BitcoinQnA/Bitcoiner.Guide/blob/main/grapheneos.md

## Perché utilizzare GrapheneOS?

I telefoni moderni sono dispositivi di tracciamento e raccolta dati del valore di 500-1000 dollari. Ogni aspetto della nostra vita passa attraverso di essi e, sfortunatamente, gran parte di questi dati viene condivisa con terze parti in qualche forma.
GrapheneOS è stato creato appositamente per ridurre questa condivisione di dati e migliorare la sicurezza del dispositivo da potenziali vettori di attacco. Non esiste un account GrapheneOS. Non ne hai bisogno per scaricare app o interagire con il sistema operativo. In poche parole, tu non sei il prodotto.

GrapheneOS fornisce una sicurezza aggiuntiva alla tua esperienza Android attraverso alcuni semplici principi fondamentali.

1. **Riduzione della superficie di attacco** - Rimuovi il codice non necessario (o il bloatware).
2. **Prevenzione dell'esposizione alle vulnerabilità** - Permetti all'utente di scegliere i compromessi con cui si sente a proprio agio.
3. **Contenimento del sandbox** - GrapheneOS rafforza i sandbox Android esistenti, limitando ulteriormente la capacità di ogni app di comunicare con il resto del tuo telefono.

Per saperne di più sui dettagli tecnici delle funzionalità di GrapheneOS, clicca [qui](https://grapheneos.org/features).

### Agevolare la transizione

Se sei stato immerso nell'ecosistema di Google o Apple per anni, il pensiero di perdere tutta quella comodità da un giorno all'altro può essere spaventoso. Ma con alcune decisioni oculate sull'installazione delle app (trattate in seguito), gran parte di questa difficoltà prevista può essere ridotta o eliminata.

Per quanto buone stiano diventando le alternative, il pensiero di un tale cambiamento può comunque essere scoraggiante. Se ti trovi in questa situazione, il mio miglior consiglio è di utilizzare il tuo nuovo dispositivo GrapheneOS insieme al tuo telefono attuale per un po' di tempo. Da lì puoi gradualmente abbandonare 2-3 app a settimana fino a quando ti ritrovi a utilizzare solo il tuo dispositivo GrapheneOS.

Se adotti questo approccio, sii severo con te stesso e interrompi il tuo affidamento sulle alternative sorvegliate il più rapidamente possibile. Noi esseri umani siamo pigri e spesso scegliamo la strada più facile. Ricorda perché hai fatto il cambio in primo luogo.

**Invece di pagare con i tuoi dati personali, hai scelto di pagare con il tuo tempo e talvolta con i tuoi soldi guadagnati a fatica (a seconda delle app alternative che installi).**

## Iniziare

Attualmente, GrapheneOS è disponibile solo per la gamma di telefoni [Google Pixel](https://grapheneos.org/faq#supported-devices) _(piuttosto ironico)_. Tuttavia, ci sono buone ragioni per questa scelta. I Pixel offrono la migliore sicurezza basata sull'hardware per completare il lavoro di rafforzamento del sistema operativo. Questo include cose come isolamenti specifici dei componenti e avvio verificato.

### Scegliere un dispositivo

Quando scegli il Pixel su cui desideri installare GrapheneOS, assicurati di verificare per quanto tempo il dispositivo continuerà a ricevere gli [aggiornamenti di sicurezza](https://support.google.com/pixelphone/answer/4457705?hl=en#zippy=%2Cpixel-xl-a-a-g-a-g) predefiniti.
Al momento della stesura, il modello Pixel 6a è il modello più economico disponibile con un buon supporto a lungo termine, garantito fino a luglio 2027. Se scegli questo modello, lo sblocco OEM non funzionerà con la versione del sistema operativo di serie. È necessario aggiornarlo alla versione di giugno 2022 o successiva tramite un aggiornamento over-the-air. Dopo averlo aggiornato, sarà anche necessario ripristinare le impostazioni di fabbrica del dispositivo per correggere lo sblocco OEM. Tutti gli altri modelli che sono sbloccati per il gestore saranno pronti per GrapheneOS appena usciti dalla confezione.

Quando scegli un dispositivo, assicurati anche di acquistare una versione sbloccata. Certi gestori come Verizon spediscono le loro unità con il bootloader bloccato, il che impedisce completamente il processo seguente.

### Installazione di GrapheneOS

Il [web installer](https://grapheneos.org/install/web) di GrapheneOS rende l'intero processo semplice e può essere completato da chiunque in meno di 10 minuti.
Le seguenti istruzioni sono una versione ridotta prese dal link sopra.

Tutto ciò di cui hai bisogno è:

- Il Pixel
- Un cavo USB per collegare il telefono al computer
- Un computer per eseguire un browser web (qualsiasi browser basato su Chromium: Chrome, Edge, Brave, ecc.)

1. Il primo passo è andare su **Impostazioni** > **Informazioni sul telefono** e toccare ripetutamente il numero di build finché non vedi che **'Modalità sviluppatore'** è attivata.
2. Successivamente, vai su **Impostazioni** > **Sistema** > **Opzioni sviluppatore** e abilita **'Sblocco OEM'**.
3. Riavvia il dispositivo e tieni premuto il pulsante del volume giù mentre il telefono si riaccende.
4. Collega il telefono al tuo laptop e, se richiesto l'autorizzazione, permetti la connessione.
5. Nella pagina del web installer, fai clic su 'Sblocca il bootloader'.
6. Vedrai quindi cambiare le opzioni del telefono. Usa il pulsante del volume per cambiare la selezione in `sblocca` e usa il pulsante di accensione per confermare.
7. Successivamente, fai clic su "scarica la versione" nella pagina del web installer.
8. Una volta completamente scaricato, passa al passaggio successivo e fai clic su 'Flash della versione'. Ciò richiederà uno o due minuti e non è necessario toccare il telefono affatto.
9. Infine, passa al passaggio successivo del web installer e fai clic su **Blocca il bootloader**. Dovrai cambiare la selezione e confermare con il pulsante di accensione allo stesso modo in cui hai fatto in precedenza nel processo.
10. Quando vedi la parola `Avvia`, confermala con il pulsante di accensione e il dispositivo si avvierà nel tuo nuovo sistema operativo privo di Google.

![image](assets/2.png)

_Dopo l'avvio iniziale e la configurazione, è buona pratica disabilitare lo sblocco OEM da Impostazioni > Sistema > Opzioni sviluppatore._

_Potresti anche voler compiere il passaggio extra, opzionale ma consigliato, di verificare l'installazione tramite l'app Auditor. Avrai bisogno di un altro telefono Android con l'app installata per completare questo passaggio. Le istruzioni per questo possono essere trovate [qui](https://attestation.app/tutorial)._

![video](https://www.youtube.com/embed/L1KZWjZVnAw)

Se questi semplici passaggi sembrano troppo complessi, potresti considerare l'acquisto di un Pixel con il software GrapheneOS [pre-installato](https://ronindojo.io/en/roninmobile). Tieni presente che stai mettendo una piccola quantità di fiducia nel fornitore.

### App preinstallate

Ora che sei pronto, potresti notare quanto sia essenziale GrapheneOS dopo la prima installazione. Di default, avrai queste app installate:

![image](assets/3.png)

Le uniche due che potresti non conoscere sono 'Auditor' e 'Vanadium'.

- L'app [Auditor](https://play.google.com/store/apps/details?id=app.attestation.auditor) utilizza funzionalità di sicurezza basate sull'hardware per convalidare l'identità di un dispositivo insieme all'autenticità e all'integrità del sistema operativo. Verificherà che il dispositivo stia eseguendo il sistema operativo di serie con il bootloader bloccato e che non siano state apportate modifiche al sistema operativo.
- [Vanadium](https://github.com/GrapheneOS/Vanadium) è una variante del browser web Chromium con privacy e sicurezza potenziate.

## Personalizzazione

Le impostazioni del telefono sono una cosa personale, ma ecco alcuni dei primi elementi che modifico quando installo GrapheneOS per sentirmi più a casa.

### Impostare uno sfondo e aggiornare il tema

Vai su Impostazioni > Sfondo e stile. Da qui:

- Aggiorna gli sfondi della schermata principale e di blocco con immagini scaricate da Internet.
- Scegli i colori di accento utilizzati in tutto l'interfaccia utente.
- Abilita il tema scuro.

### Mostra la percentuale della batteria

Vai su **Impostazioni** > **Batteria**, quindi abilita **Mostra percentuale batteria** nella barra di stato.

### Importa contatti

**Da un altro telefono Android** - Vai all'app Contatti e cerca l'opzione Esporta in formato VCF.

**Da iOS** - Usa un'app come Export Contact e utilizza l'opzione di esportazione 'vCard' per esportare un file VCF.
Una volta ottenuto il file VCF, puoi trasferirlo sul tuo dispositivo GrapheneOS tramite un'opzione di archiviazione esterna come una scheda microSD o una chiavetta USB. Se non ne hai a disposizione, puoi optare per la condivisione tramite una delle molte app elencate di seguito.

![image](assets/4.png)

## App alternative

Per rendere il tuo telefono utile, vorrai installare alcune applicazioni! Le opzioni seguenti sono incluse perché le ho usate personalmente o perché ricevono forti raccomandazioni dalla comunità della privacy. Ci sono molte altre ottime alternative disponibili che non sono menzionate, e [Awesome Privacy](https://awesome-privacy.xyz) offre un elenco estremamente completo di applicazioni per la privacy per tutti i tipi di dispositivi.

Il fatto che un'app sia un software gratuito e open source (FOSS) non significa che sia esente da potenziali falle nella privacy. Usa [Exodus](https://reports.exodus-privacy.eu.org/en/) per vedere come le tue app preferite si comportano rispetto alle loro verifiche sulla privacy.

### F-Droid

[F-Droid](https://f-droid.org/) è un catalogo installabile di applicazioni FOSS per Android. Il client facilita la navigazione, l'installazione e l'aggiornamento delle applicazioni sul tuo dispositivo. Vale la pena menzionare che gli aggiornamenti tramite F-Droid possono essere talvolta più lenti rispetto ad altri app store. Questo dipende principalmente dal fatto che l'app venga trovata tramite il repository principale di F-Droid o uno personalizzato.

Per installare F-Droid, basta andare sul loro sito web tramite un browser sul tuo telefono GrapheneOS e toccare il pulsante di download. Questo scaricherà un file `.apk`. Ti verrà quindi chiesto se desideri installare l'app.

Oltre alle applicazioni presenti nel repository predefinito di F-Droid, molti progetti open source ospiteranno anche il proprio repository che può essere aggiunto nelle impostazioni dell'app F-Droid. Se questo è il caso, il progetto in questione ti guiderà attraverso i passaggi molto semplici necessari per farlo sul loro sito web.

![image](assets/5.png)

### Aurora Store

[Aurora Store](https://auroraoss.com/) è una versione FOSS del Google Play Store. Aurora ha un aspetto molto simile al tradizionale Play Store e ti permette di scaricare e aggiornare qualsiasi app che normalmente troveresti tramite l'opzione Google.
La caratteristica principale di Aurora è l'accesso anonimo. Ciò significa che puoi scaricare tutte le tue app preferite che non sono disponibili tramite F-Droid o APK diretto, senza dover effettuare l'accesso al tuo account Google.

Prima di affrettarti a rendere questa la tua opzione di installazione predefinita, ricorda che molte delle applicazioni da cui stiamo cercando di allontanarci sono state installate dal Play Store. Il fatto che siano accessibili da Aurora non cambia il fatto che alcune potrebbero avere funzionalità di tracciamento incorporate. Non sarà sempre possibile, ma ogni volta che puoi, cerca un'alternativa su F-Droid prima di scaricare tramite Aurora.

Per installare Aurora, cerca semplicemente 'Aurora Store' su F-Droid.

Aurora ha anche alcuni potenziali vettori di attacco, poiché gli "account anonimi" sono effettivamente creati e controllati da Aurora. Potrebbero, in teoria, fornire aggiornamenti maligni o installare app sul tuo telefono, anche se dovresti comunque accettare la richiesta di installazione sul dispositivo. Aurora a volte ha anche problemi con le app che non vengono visualizzate a causa di errori di lettura della regione e del dispositivo. Questo problema di solito può essere risolto seguendo i passaggi di seguito.

**Consiglio principale** - A volte Aurora Store può avere limitazioni di velocità che limitano la tua capacità di cercare e installare app. Per aggirare questo problema, vai su **Impostazioni** > **App** > **Aurora** > **Apri per impostazione predefinita**, quindi aggiungi il dominio `play.google.com`. Ora, ogni volta che accedi al sito web di un prodotto o servizio che ha il link 'Scarica tramite Play Store', toccarlo aprirà quell'app all'interno di Aurora per poterla scaricare.

![image](assets/6.png)

### Download APK

Le app su Android possono anche essere scaricate e installate tramite un file `.apk`. Questa è un'ottima alternativa che non richiede app di terze parti, basta scaricare il file direttamente dal sito del progetto o del servizio o dal repository GitHub.

Il lato negativo di questo approccio è che non riceverai aggiornamenti automatici, quindi dovrai monitorare i canali di comunicazione del servizio per conoscere le nuove versioni. Tuttavia, c'è un ottimo progetto chiamato Obtainium che mira a risolvere questo problema. [Obtainium](https://github.com/ImranR98/Obtainium) ti permette di installare e aggiornare app open-source direttamente dalle pagine delle loro versioni e ricevere notifiche quando sono disponibili nuove versioni.

![image](assets/7.png)

### App Web

Per i momenti in cui potresti voler utilizzare un servizio in modo sporadico e non desideri scaricare un'applicazione nativa, puoi semplicemente accedere alla versione web. Oggi molti siti web offrono anche il supporto per Progressive Web App (PWA). In questo caso, puoi aggiungere un segnalibro a un sito web specifico (ad esempio Twitter.com) nella schermata principale del tuo telefono. Quando tocchi sull'icona, si aprirà come un'applicazione a schermo intero senza le solite distrazioni che si trovano nell'esperienza tipica del browser. Puoi vedere un esempio di come appare ciò di seguito.

Per ottenere questo risultato in Vanadium, il browser nativo di GrapheneOS, basta navigare sul sito web scelto, toccare i tre punti verticali nell'angolo in alto a destra dello schermo e quindi toccare **'Aggiungi alla schermata principale'**.

L'unico svantaggio di questo approccio è che, essendo solo una pagina web segnalibro, non riceverai alcuna forma di notifica. Anche se alcuni potrebbero considerarlo un aspetto positivo!

![image](assets/8.png)

### Browser Web

Non puoi davvero sbagliare con l'opzione preconfezionata, Vanadium. L'app si comporta in modo identico a qualsiasi altro browser mobile che ho provato e non ho mai avuto problemi di compatibilità.
Per i momenti in cui hai bisogno di accedere ai siti nativi `.onion` di Tor, puoi scaricare direttamente l'APK del Tor Browser dal loro [sito web](https://www.torproject.org/download/#android) o tramite F-Droid.

### VPN

Per proteggere la tua attività online dal tuo ISP che spia, un'app di rete privata virtuale (VPN) è una buona opzione. Una VPN invia il tuo traffico internet in un tunnel crittografato verso un indirizzo IP condiviso controllato dal provider del servizio VPN per garantire che l'attività del tuo dispositivo non possa essere collegata a te.

Le seguenti sono 3 opzioni rispettate che ti consentono di pagare il servizio in Bitcoin e senza fornire alcuna informazione personale. Tutte e 3 le opzioni sono disponibili tramite F-Droid.

- [Mullvad](https://f-droid.org/packages/net.mullvad.mullvadvpn/)
- [Proton](https://f-droid.org/en/packages/ch.protonvpn.android/)
- [iVPN](https://f-droid.org/en/packages/net.ivpn.client/)

### Messaggistica

Negli ultimi anni le soluzioni di messaggistica crittografata sono diventate abbondanti. Il problema rimane però che puoi avere la migliore e più privata opzione installata sul tuo telefono, ma se non hai contatti che la utilizzano, qual è il punto?

La maggior parte delle persone che non sono interessate alla privacy probabilmente utilizza WhatsApp o iMessage. Il primo può essere scaricato tramite Aurora Store, ma il secondo non funzionerà su GrapheneOS (ovviamente!).

- [Signal](https://signal.org/) è uno dei messaggeri end-to-end crittografati (E2EE) più popolari che ha un solido track record e un ricco set di funzionalità. Signal richiede un numero di telefono per la registrazione, quindi se hai intenzione di chattare con persone che preferiresti non conoscessero il tuo numero di telefono, forse dovresti considerare alcune alternative. Signal deve essere scaricato tramite Aurora Store.
- [Simplex](https://f-droid.org/en/packages/chat.simplex.app/) è un messaggero E2EE abbastanza nuovo. Non ha un ID utente, non richiede un numero di telefono o informazioni personali. Le persone ti trovano scansionando il tuo codice QR personale o visitando il tuo link unico. Simplex consente anche agli utenti avanzati di eseguire il proprio server per ridurre ulteriormente la dipendenza da qualsiasi entità centralizzata. Simplex non ha un client desktop, quindi potrebbe non essere adatto se la compatibilità multi-dispositivo è una priorità. Simplex per Android è disponibile tramite F-Droid.
- [Threema](https://threema.ch/en/faq/libre_installation) offre un'esperienza simile a Simplex, ma è presente da più tempo e di conseguenza sembra un po' più rifinito. Threema non è gratuito, una licenza a vita costa $4.99 e può essere acquistata con Bitcoin. Threema offre un client web e applicazioni desktop native. L'applicazione Android è disponibile tramite F-Droid.
- [Telegram FOSS](https://f-droid.org/en/packages/org.telegram.messenger/) è un fork non ufficiale FOSS dell'app ufficiale di Telegram per Android. Telegram ha chat segrete E2EE, ma l'opzione predefinita non è privata. Telegram FOSS può essere scaricato da F-Droid.

![image](assets/9.png)

### Media

- [Spotube](https://f-droid.org/packages/oss.krtirtho.spotube/) è un client Spotify multi-piattaforma che non richiede un account Premium. Spotube è disponibile tramite F-Droid.
- [ViMusic](https://f-droid.org/en/packages/it.vfsfitvnm.vimusic/) è un'applicazione fantastica per lo streaming di qualsiasi musica da YouTube, gratuitamente. ViMusic è disponibile su F-Droid.
- [Newpipe](https://f-droid.org/packages/org.schabi.newpipe/) offre un'esperienza di YouTube senza fastidiosi annunci pubblicitari e autorizzazioni discutibili. Con NewPipe puoi iscriverti ai canali, ascoltare in background e persino scaricare per la visualizzazione offline. NewPipe è accessibile tramite F-Droid.
- [AntennaPod](https://f-droid.org/packages/de.danoeh.antennapod/) è un lettore di podcast che ti permette di iscriverti e gestire tutti i tuoi show preferiti. AntennaPod è disponibile tramite F-Droid.

![image](assets/11.png)

### Mappe

Se desideri assistenza vocale durante la guida e l'utilizzo di un'app di mappe su GrapheneOS, dovrai installare [RHVoice](https://rhvoice.org/installation/) e [configurarlo](https://discuss.grapheneos.org/d/2488-organic-maps-app-voice-instructions-are-not-available).

- [Magic Earth](https://www.magicearth.com/) è un'alternativa alle mappe che supporta la navigazione passo-passo, mappe 3D e offline. Magic Earth può essere scaricato da Aurora Store.
- [Organic Maps](https://f-droid.org/en/packages/app.organicmaps/) è un'alternativa alle mappe per viaggiatori, turisti, escursionisti e ciclisti basata sui dati di OpenStreetMap generati dalla comunità. È un'app open source incentrata sulla privacy, un fork di Maps.me (precedentemente noto come MapsWithMe). Supporta il 100% delle funzionalità senza connessione Internet attiva e può essere scaricato da F-Droid.
- [OsmAnd](https://f-droid.org/en/packages/net.osmand.plus/) è un'altra ottima alternativa alle mappe che supporta tutte le funzionalità menzionate in precedenza.

![image](assets/13.png)

### Email

- [Proton Mail](https://proton.me/mail) offre un servizio di posta elettronica privato gratuito che supporta l'E2EE verificato. Proton offre anche una versione a pagamento che supporta domini personalizzati e [aliasing](https://proton.me/support/creating-aliases). Proton Mail può essere scaricato come APK diretto o tramite Aurora.
- [Tutanota](https://tutanota.com/) offre le stesse funzionalità di Proton Mail, inclusi servizi a pagamento opzionali e può essere scaricato come APK diretto o tramite F-Droid.
- [K-9 Mail](https://f-droid.org/en/packages/com.fsck.k9/) è un client di posta elettronica open source che funziona con praticamente tutti i provider di posta elettronica. Supporta account multipli, una casella di posta unificata e lo standard di crittografia OpenPGP.

![image](assets/15.png)

### Produttività

- [Syncthing](https://f-droid.org/packages/com.nutomic.syncthingandroid/) è un programma di sincronizzazione dei file. Sincronizza i file tra due o più dispositivi in tempo reale, protetti in modo sicuro dagli occhi indiscreti. I tuoi dati sono solo tuoi e meriti di scegliere dove vengono archiviati, se vengono condivisi con terze parti e come vengono trasmessi su Internet. Syncthing è disponibile tramite F-Droid.
- [KDE Connect](https://f-droid.org/packages/org.kde.kdeconnect_tp/) permette a tutti i tuoi dispositivi di comunicare facilmente tra loro quando sono connessi alla tua rete domestica. Puoi inviare facilmente file, foto, dati degli appunti su tutti i tuoi dispositivi (anche su iOS!). KDE Connect può essere scaricato da F-Droid.
- [Notesnook](https://f-droid.org/en/packages/com.streetwriters.notesnook/) è un'applicazione di appunti E2EE per sincronizzare i tuoi pensieri e liste di cose da fare su tutti i tuoi dispositivi. Il loro piano gratuito dovrebbe coprire la maggior parte dei casi d'uso personali. Notesnook è disponibile su F-Droid.
- [Standard Notes](https://f-droid.org/en/packages/com.standardnotes/) è molto simile a Notesnook, ma richiede un piano a pagamento per corrispondere alle funzionalità offerte. Standard Notes è disponibile tramite F-Droid.
- [Anysoft Keyboard](https://f-droid.org/packages/com.menny.android.anysoftkeyboard/) è un'app di tastiera che ti consente di personalizzare praticamente tutto ciò che riguarda la digitazione sul tuo telefono. Può essere scaricato tramite F-Droid.
- [GBoard](https://play.google.com/store/apps/details?id=com.google.android.inputmethod.latin&hl=en&gl=US) è l'app di tastiera predefinita di Google. Sulla base della mia esperienza, offre di gran lunga la migliore esperienza di digitazione e scorrimento. Se scarichi questa app, assicurati di disabilitare completamente tutte le autorizzazioni relative alla rete. Può essere scaricato tramite Aurora.

![image](assets/17.png)

### Stile di vita

- [Geometric Weather](https://f-droid.org/en/packages/wangdaye.com.geometricweather/) è un'app meteo Open Source dal design accattivante disponibile tramite F-Droid. Supporta anche molti formati diversi di widget, in modo da poter visualizzare il meteo nella tua posizione preferita direttamente dalla schermata principale.
- [Translate You](https://f-droid.org/packages/com.bnyro.translate/) è un'app di traduzione Open Source che supporta più di 200 lingue, garantendo la privacy dell'utente. Translate You è disponibile tramite F-Droid.
- [Proton Calendar](https://proton.me/calendar/download) è un calendario semplice da usare con crittografia end-to-end che si integra perfettamente con i tuoi account email di Proton. Proton Calendar può essere scaricato come APK o tramite il negozio Aurora.
- [PassAndroid](https://f-droid.org/en/packages/org.ligi.passandroid/) è un'app per visualizzare e archiviare carte d'imbarco, coupon, biglietti del cinema e tessere di associazioni, ecc. Basta scaricare il file `pkpass` o `espass` pertinente e aprirlo con l'app. PassAndroid è disponibile tramite F-Droid.

![image](assets/19.png)

### Sicurezza/Privacy

- [Bitwarden](https://mobileapp.bitwarden.com/fdroid/) offre una soluzione gratuita e E2EE per la gestione delle password su tutte le tue dispositivi. Il loro servizio a pagamento consente di integrare i codici 2FA nell'app. Il server di Bitwarden può essere auto-ospitato e l'app Android è disponibile tramite F-Droid.
- [Proton Pass](https://proton.me/pass/download) offre un servizio gratuito simile a Bitwarden, ma i clienti di [Proton Unlimited](https://proton.me/pricing) possono accedere a funzionalità avanzate aggiuntive. Proton Pass è disponibile tramite APK o Aurora.
- [FreeOTP](https://f-droid.org/packages/org.fedorahosted.freeotp/) è un'applicazione di autenticazione a due fattori per sistemi che utilizzano protocolli di password monouso. I token possono essere aggiunti facilmente scansionando un codice QR. FreeOTP è disponibile tramite F-Droid.
- [Aegis](https://f-droid.org/en/packages/com.beemdevelopment.aegis/) è un'app gratuita, sicura e Open Source per Android per gestire i token di verifica in due passaggi per i tuoi servizi online. Aegis è disponibile tramite F-Droid.
- [Cryptomator](https://f-droid.org/en/packages/org.cryptomator.lite/) è un servizio a pagamento, multi-piattaforma, che crittografa i tuoi dati in locale in modo da poterli caricare in modo sicuro sul tuo servizio cloud preferito. Cryptomator può essere scaricato tramite F-Droid.
  ![image](assets/21.png)

### Soluzioni Cloud

- [Proton Drive](https://proton.me/drive/download) è una soluzione cloud a pagamento con crittografia end-to-end per il backup e l'archiviazione di tutti i tuoi file. Al momento della stesura, hanno appena annunciato un client desktop per Windows, ma gli utenti Mac e Linux devono continuare a utilizzare la versione web per sincronizzare dai loro computer (per ora). Il client Android è disponibile come APK o tramite Aurora.
- [Skiff](https://skiff.com/download) offre anche un servizio di archiviazione cloud a pagamento con crittografia end-to-end e strumenti di collaborazione sui file. Offrono un client desktop per Mac e Windows (oltre a un'app web) e i loro client Android devono essere scaricati da Aurora.
- [Nextcloud](https://f-droid.org/en/packages/com.nextcloud.client/) offre una soluzione cloud completa per la collaborazione, la sincronizzazione tra dispositivi e l'archiviazione dei file. Gli utenti più esperti possono scegliere di ospitare il loro software gratuito e open source su qualsiasi hardware desiderino. I client Android possono essere scaricati tramite F-Droid.
- [Cryptpad](https://cryptpad.fr/) offre un'alternativa gratuita basata sul web a Google Docs con crittografia end-to-end.

![image](assets/23.png)

## Gli Svantaggi

Le alternative open source e rispettose della privacy alle applicazioni dei conglomerati tecnologici a cui ti sei abituato sono numerose, e alcune di esse sono spesso migliori delle alternative closed source piene di spyware.

Tuttavia, passando a GrapheneOS, ci sono alcuni comfort che devi rinunciare a causa della mancanza di alternative. Questi includono:

- **Apple CarPlay/Android Auto** - Dovrai continuare a utilizzare il buon vecchio Bluetooth, USB o Aux.
- **Apple/Google Pay** - Praticamente tutti portano il portafoglio con sé comunque!
- **App bancarie** - Non è che non funzionino affatto. Alcune funzionano perfettamente. Altre funzionano solo con Google Play Services abilitato (leggi di più a riguardo qui sotto) e altre semplicemente non funzionano affatto. Leggi il rapporto sulla tua banca [qui](https://privsec.dev/posts/android/banking-applications-compatibility-with-grapheneos/) per vedere lo stato attuale. Non temere se la tua banca è nella lista delle app che non funzionano, ricorda che puoi semplicemente salvare l'URL come app web nella tua schermata principale.
- **Notifiche push** - La maggior parte delle applicazioni che inviano aggiornamenti quando non si utilizza un'app specifica lo fanno tramite Google Play Services. Questi non sono installati di default su GrapheneOS, quindi se ti accorgi di non essere notificato immediatamente quando un amico ti invia una e-mail, è probabilmente per questo motivo. La buona notizia è che alcune delle app menzionate sopra hanno implementato la propria connessione in background per controllare periodicamente gli aggiornamenti e quindi inviarti una notifica quando necessario.

### Google Play in un ambiente sandbox

> 'GrapheneOS ha uno strato di compatibilità che offre la possibilità di installare e utilizzare le versioni ufficiali di Google Play nell'ambiente sandbox standard. Google Play non riceve assolutamente alcun accesso o privilegio speciale su GrapheneOS, a differenza di bypassare l'ambiente sandbox dell'app e ricevere un'enorme quantità di accesso altamente privilegiato.'
> Se trovi che semplicemente non puoi vivere senza quelle notifiche push per la tua app preferita o che una certa app "indispensabile" è inutile senza Play Services, GrapheneOS ti permette di installare questi servizi in un ambiente completamente sandboxed. Una volta installati, questi servizi non richiedono un account Google per funzionare e le autorizzazioni di ognuno possono essere controllate in modo rigoroso.
> Prima di affrettarti ad installarli il primo giorno, ti consiglio di vedere fino a che punto riesci senza di essi. Probabilmente sarai sorpreso di quanti app funzionano perfettamente normalmente senza di essi.

Se desideri installarli, basta toccare l'applicazione pre-installata "App" seguita da "Google Play Services". Considera di installarli insieme a quelle app meno private di cui non puoi fare a meno, all'interno di un profilo utente completamente separato per fornire un ulteriore livello di segregazione dal resto del tuo telefono.

![image](assets/24.png)

### Profili

GrapheneOS ti permette di avere un'esperienza telefonica separata, all'interno del tuo telefono. I profili aggiuntivi possono installare le proprie app e servizi e non possono accedere a file o dati dell'account proprietario.
Se hai solo una o due di quelle app indispensabili che richiedono Play Services, ma vengono utilizzate solo molto raramente, installarle insieme a Play Services in un profilo separato potrebbe essere un'ottima idea per rafforzare ulteriormente eventuali implicazioni sulla privacy che rimangono nel profilo proprietario.

Puoi leggere di più su questo caso d'uso [qui](https://discuss.grapheneos.org/d/168-ideas-for-user-profiles/2).

Se decidi di aggiungere un profilo separato per adattarlo al tuo caso d'uso, l'app [Insular](https://f-droid.org/en/packages/com.oasisfeng.island.fdroid/) potrebbe esserti utile. Insular ti permette di clonare facilmente una delle tue app esistenti nel nuovo profilo senza dover passare attraverso le tradizionali route di installazione descritte in precedenza in questa guida. Insular ti permette anche di "congelare" rapidamente qualsiasi di queste app per disabilitare completamente tutti i servizi in background dell'app.

![image](assets/25.png)

### e-SIM

Se vuoi portare la tua privacy telefonica al livello successivo e avere un servizio cellulare separato dalla tua identità nel mondo reale, potrebbe interessarti una eSIM. Una eSIM è una SIM virtuale che puoi acquistare online e aggiungere al tuo telefono tramite un codice QR. Aziende che offrono tali servizi che possono essere pagati in modo anonimo con Bitcoin includono [Silent.Link](https://silent.link/) e [Bitrefill](https://www.bitrefill.com/gb/en/esims/).

Le eSIM non dovrebbero essere considerate come una panacea completa per la privacy telefonica. Possono essere uno strumento utile nelle mani giuste, ma ti prego di fare le tue ricerche sui compromessi nell'uso di qualsiasi tipo di servizio cellulare se la tua intenzione è di andare completamente "fuori rete".

I Play Services sandboxed devono essere installati per la fornitura di eSIM in GrapheneOS.

## Backup

Dopo aver configurato il tuo nuovo telefono Pixel senza Google, è una buona idea creare un backup. Questo backup ti permetterà di ripristinare il telefono in uno stato identico nel caso in cui lo perdi o venga smarrito/rubato.

Puoi scegliere di salvare il file di backup su qualsiasi supporto di archiviazione esterno o su una soluzione cloud self-hosted come Nextcloud, anche se alcuni utenti riportano livelli di successo variabili con quest'ultima opzione.

Per creare il tuo primo backup:

1. Vai su **Impostazioni** > **Sistema** > **Backup**, quindi annota il tuo codice di ripristino di 12 parole. Questo codice è necessario per decrittare il file di backup in una data successiva. Perdi il codice, perdi l'accesso al backup del tuo telefono.
2. Successivamente, scegli la posizione di archiviazione. Consiglio un'unità USB esterna o una scheda microSD di grado industriale.
3. Scegli i dati da eseguire il backup. Se hai spazio sul supporto di archiviazione specificato, consiglio di selezionare tutto.
4. Tocca i tre puntini in alto a destra e scegli **Esegui backup ora**.

![image](assets/26.png)

Ricorda che se stai effettuando backup offline su supporti di archiviazione esterni, ha senso completare regolarmente questo passaggio per assicurarti che eventuali importanti aggiornamenti recenti del tuo telefono non vengano persi nel caso peggiore.

![video](https://www.youtube.com/embed/eyWmcItzisk)

## Conclusioni

Negli ultimi anni, il software GrapheneOS è maturato significativamente. È più stabile e compatibile che mai. Abbinando questo all'ecosistema di app Open Source e rispettose della privacy in piena espansione, GrapheneOS rappresenta un'alternativa veramente valida ad Android o iOS di serie, anche per persone "normali" come te!

Violazioni dei dati e sorveglianza di massa sono così comuni nel mondo di oggi che quasi non fanno più notizia. Sta a te proteggerti. Ci saranno adattamenti e sacrifici da fare lungo il cammino, ma ridurre la tua esposizione a tali violazioni non è affatto difficile come pensi che sia.

Spero che questa guida ti aiuti nel tuo percorso. Se hai trovato utile questa guida e desideri supportare il mio lavoro, considera di inviare una [donazione](/tips).

Se sei un utente di GrapheneOS esistente o diventi tale a seguito di questa guida, considera di [donare](https://grapheneos.org/donate) per sostenere il loro importante lavoro.

### Scopri di più

GrapheneOS è una tana di coniglio in cui chiunque potrebbe facilmente passare settimane. C'è così tanto da imparare e sperimentare per adattare l'esperienza alle tue esigenze e modelli di minaccia. Di seguito trovi alcuni link dove puoi continuare il tuo viaggio:

- [Guida ufficiale all'uso di GrapheneOS](https://grapheneos.org/usage) - Sito web ufficiale
- [Forum di GrapheneOS](https://discuss.grapheneos.org/) - Sito web ufficiale
- [Masterclass delle impostazioni di GrapheneOS](https://www.youtube.com/watch?app=desktop&v=GLJyD9MJgIQ) - Video di 'The Privacy Wayfinder'
- [Podcast generale di GrapheneOS](https://www.youtube.com/watch?app=desktop&v=UCPX0mFFRNA) - Podcast di 'Watchman Privacy'

Merito completo a: https://github.com/BitcoinQnA/Bitcoiner.Guide/blob/main/grapheneos.md
