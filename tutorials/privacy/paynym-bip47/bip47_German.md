---
name: BIP47 - PayNym

description: Wie PayNym funktioniert
---

# BIP47, das hässliche Entlein.

> "Es ist zu groß", sagten sie alle, und der Truthahn, der mit Sporen geboren wurde und sich für einen Kaiser hielt, blähte sich wie ein Schiff mit vollen Segeln auf und ging mit großer Wut und roten Augen direkt auf ihn zu. Das arme Entlein wusste nicht, ob es stehen bleiben oder weitergehen sollte: Es war sehr traurig, von allen Enten im Hof verspottet zu werden.

![BIP47, das hässliche Entlein Illustration](assets/1.png)

Eine der größten Schwachstellen im Bitcoin-Protokoll ist die Wiederverwendung von Adressen. Die Transparenz und die Verteilung des Netzwerks machen diese Praxis gefährlich für die Privatsphäre des Benutzers. Um Probleme damit zu vermeiden, wird empfohlen, für jede neue eingehende Zahlung an eine Brieftasche eine neue leere Empfangsadresse zu verwenden, was in einigen Fällen kompliziert sein kann.

Dieser Kompromiss ist so alt wie das White Paper. Satoshi hat uns bereits in seinem Ende 2008 veröffentlichten Werk vor diesem Risiko gewarnt:

> "Als zusätzliche Firewall könnte für jede Transaktion ein neues Schlüsselpaar verwendet werden, um sie nicht mit einem gemeinsamen Eigentümer zu verknüpfen."

Es gibt viele Lösungen, um mehrere Zahlungen zu empfangen, ohne die Adresse wiederzuverwenden. Jede Lösung hat ihre eigenen Kompromisse und Nachteile. Eine davon ist das [BIP47](https://github.com/bitcoin/bips/blob/master/bip-0047.mediawiki), ein Vorschlag von Justus Ranvier aus dem Jahr 2015, der es ermöglicht, wiederverwendbare Zahlungscodes zu generieren. Das Ziel ist es, mehrere Transaktionen an eine Person durchzuführen, ohne dabei die Adresse wiederzuverwenden.

Anfangs wurde dieser Vorschlag von einem Teil der Community verachtet und wurde nie zu Bitcoin Core hinzugefügt. Einige Softwareprogramme haben sich jedoch dafür entschieden, es auf eigene Faust zu implementieren. So hat [Samourai Wallet](https://samouraiwallet.com/) seine eigene Implementierung von BIP47 entwickelt: PayNym. Heute ist diese Implementierung natürlich auf Samourai Wallet für Smartphones verfügbar, aber auch auf [Sparrow Wallet](https://sparrowwallet.com/) für PCs.

Im Laufe der Zeit hat Samourai neue Funktionen entwickelt, die direkt mit PayNym zusammenhängen. Es gibt jetzt ein ganzes Ökosystem von Tools, die auf PayNym und BIP47 basieren und die Privatsphäre des Benutzers optimieren.
Dans diesem Artikel erfahren Sie das Prinzip von BIP47 und PayNym, die Mechanismen dieser Protokolle und die daraus resultierenden praktischen Anwendungen. Ich werde nur auf die erste Version von BIP47 eingehen, die derzeit für PayNym verwendet wird, aber die Versionen 2, 3 und 4 funktionieren praktisch auf die gleiche Weise.

> Der einzige wesentliche Unterschied liegt in der Benachrichtigungstransaktion. Version 1 verwendet eine einfache Adresse mit OP_RETURN für die Benachrichtigung, Version 2 verwendet ein Multisig-Skript (Bloom-Multisig) mit OP_RETURN und Version 3 und 4 verwenden einfach ein Multisig-Skript (Cfilter-Multisig). Die in diesem Artikel behandelten Mechanismen, insbesondere die untersuchten kryptographischen Methoden, sind daher auf alle vier Versionen anwendbar. Derzeit verwendet die PayNym-Implementierung in Samourai Wallet und Sparrow die erste Version von BIP47.

## Inhaltsverzeichnis:

1. Das Problem der Adresswiederverwendung.
2. Prinzipien von BIP47 und PayNym.
3. Tutorials: Verwendung von PayNym.
   - Erstellen einer BIP47-Transaktion mit Samourai Wallet.
   - Erstellen einer BIP47-Transaktion mit Sparrow Wallet.
4. Die Funktionsweise von BIP47.
   - Der wiederverwendbare Zahlungscode.
   - Die kryptographische Methode: Der Diffie-Hellman-Schlüsselaustausch auf elliptischen Kurven (ECDH).
   - Die Benachrichtigungstransaktion.
   - Erstellen der Benachrichtigungstransaktion.
   - Empfang der Benachrichtigungstransaktion.
   - Die BIP47-Zahlungstransaktion.
   - Empfang der BIP47-Zahlung und Ableitung des privaten Schlüssels.
   - Rückerstattung der BIP47-Zahlung.
5. Abgeleitete Verwendungen von PayNym.
6. Meine persönliche Meinung zu BIP47.

## Das Problem der Adresswiederverwendung.

Eine Empfangsadresse wird verwendet, um Bitcoins zu empfangen. Sie wird aus einem öffentlichen Schlüssel generiert, indem er gehasht und einem spezifischen Format unterzogen wird. Dadurch wird eine neue Ausgabebeschränkung für eine Münze erstellt, um den Eigentümer zu ändern.

> Um mehr über die Generierung einer Empfangsadresse zu erfahren, empfehle ich Ihnen, den letzten Teil dieses Artikels zu lesen: Das Bitcoin-Wallet - Auszug aus dem eBook Bitcoin Démocratisé 2.

Außerdem haben Sie sicherlich schon von einem erfahrenen Bitcoiner gehört, dass Empfangsadressen nur einmal verwendet werden sollten und dass Sie daher für jede neue eingehende Zahlung in Ihre Brieftasche eine neue Adresse generieren sollten. Aber warum?
Fondamentalmente stellt die Wiederverwendung einer Adresse Ihre Gelder nicht direkt in Gefahr. Die Verwendung von Kryptographie auf elliptischen Kurven ermöglicht es dem Netzwerk, nachzuweisen, dass Sie im Besitz eines privaten Schlüssels sind, ohne diesen Schlüssel preiszugeben. Sie können also mehrere verschiedene UTXOs auf derselben Adresse sperren und zu verschiedenen Zeitpunkten ausgeben. Wenn Sie den privaten Schlüssel, der mit dieser Adresse verbunden ist, nicht preisgeben, kann niemand auf Ihre Gelder zugreifen. Das Problem der Adresswiederverwendung betrifft eher die Privatsphäre.

Wie bereits in der Einleitung erwähnt, ermöglichen die Transparenz und die Verteilung des Bitcoin-Netzwerks jedem Benutzer, der Zugriff auf einen Knoten hat, die Beobachtung der Transaktionen des Zahlungssystems. Dadurch kann er die verschiedenen Guthaben der Adressen sehen. Satoshi Nakamoto erwähnte dann die Möglichkeit, neue Schlüsselpaare und damit neue Adressen für jede neue eingehende Zahlung an eine Brieftasche zu generieren. Das Ziel wäre es, eine zusätzliche Firewall zu haben, falls eine Verbindung zwischen der Identität des Benutzers und einem seiner Schlüsselpaare hergestellt wird.

Heutzutage ist die Verwendung leerer Adressen mit dem Vorhandensein von Chain-Analyseunternehmen und der Entwicklung von KYC keine zusätzliche Firewall mehr, sondern eine Verpflichtung für jeden, der sich auch nur minimal um seine Privatsphäre kümmert.

Die Suche nach Privatsphäre ist kein Komfort oder Fantasie eines maximalistischen Bitcoiners. Es handelt sich um einen spezifischen Parameter, der direkt Ihre persönliche Sicherheit und die Sicherung Ihrer Gelder betrifft. Um Ihnen dies verständlich zu machen, hier ein sehr konkretes Beispiel:

- Bob kauft Bitcoin im DCA (Dollar-Cost-Averaging)-Verfahren, d.h. er erwirbt regelmäßig eine kleine Menge Bitcoin, um den Einstiegspreis zu glätten. Bob sendet die gekauften Gelder systematisch an dieselbe Empfangsadresse. Er kauft jede Woche 0,01 Bitcoin und sendet sie an diese Adresse. Nach zwei Jahren hat Bob einen ganzen Bitcoin auf dieser Adresse angesammelt.

- Der Bäcker an seiner Ecke akzeptiert Bitcoin-Zahlungen. Bob ist glücklich, Bitcoin ausgeben zu können, und geht, um sein Baguette in Sats zu kaufen. Um zu bezahlen, verwendet er die mit seiner Adresse gesperrten Gelder. Sein Bäcker weiß nun, dass er einen Bitcoin besitzt. Dieser hohe Betrag könnte Neider auf den Plan rufen, und Bob könnte potenziell später einem physischen Angriff ausgesetzt sein.

Die Wiederverwendung einer Adresse ermöglicht es einem Beobachter daher, eine unbestreitbare Verbindung zwischen Ihren verschiedenen UTXOs und manchmal zwischen Ihrer Identität und Ihrer gesamten Brieftasche herzustellen.
'C'est pour cette raison que la majorité des logiciels de portefeuille Bitcoin vous génèrent automatiquement une nouvelle adresse de réception lorsque vous cliquez sur le bouton « Recevoir ». Pour l'utilisateur régulier, prendre l'habitude d'utiliser des adresses vierges n'est de ce fait pas d'un grand inconvénient. En revanche, pour un commerce en ligne, un exchange ou une campagne de donation, cette contrainte peut rapidement devenir ingérable.

Il existe de nombreuses solutions pour ces organisations. Chacune d'entre elles dispose de ses avantages et de ses inconvénients, mais à ce jour, et comme nous le verrons plus loin, le BIP47 se différencie réellement des autres.

Ce problème de la réutilisation d'adresse est loin d'être négligeable sur Bitcoin. Comme vous pouvez le voir sur le graphique ci-dessous extrait du site [oxt.me](http://oxt.me/), le taux global de réutilisation d'adresse par les utilisateurs de Bitcoin est actuellement de 52% :
Graphique OXT.me évolution du taux global de réutilisation d'adresses sur le réseau Bitcoin.

![image](assets/2.png)

Crédit : https://oxt.me/charts

La majorité de ces réutilisations provient des exchanges qui, pour des raisons d'efficacité et de facilité, réutilisent une même adresse de nombreuses fois. À ce jour, le BIP47 serait la meilleure solution pour endiguer ce phénomène chez les exchanges. Cela permettrait d'engager à la baisse ce taux global de réutilisation d'adresse, sans pour autant occasionner trop de frictions pour ces entités.

Cette mesure globale sur l'ensemble du réseau est une donnée particulièrement cohérente dans ce cas-là. En effet, la réutilisation d'adresse n'est pas uniquement un problème pour la personne qui réalise ce type de pratique, mais également pour toute personne qui réalise des transactions avec celle-ci. La perte de confidentialité sur Bitcoin agit comme virus, et se propage d'utilisateurs en utilisateurs. Étudier une mesure globale sur toutes les transactions du réseau nous permet de prendre conscience de l'ampleur de ce phénomène.

## Principes du BIP47 et de PayNym.

BIP47 vise à proposer une façon simple de recevoir de nombreux paiements tout en ne faisant pas de réutilisation d'adresse. Son fonctionnement est fondé sur l'utilisation d'un code de paiement réutilisable.

Ainsi, plusieurs émetteurs pourront envoyer plusieurs paiements vers un unique code de paiement réutilisable d'un autre utilisateur, sans que le destinataire ait besoin de transmettre une nouvelle adresse vierge pour chaque nouvelle transaction.

Un utilisateur peut alors communiquer librement son code de paiement (sur les réseaux sociaux, sur son site web...) sans risque de perte de confidentialité, contrairement à une adresse de réception classique ou à une clé publique.'
Um einen Austausch durchzuführen, müssen beide Benutzer über eine Bitcoin-Wallet mit einer Implementierung von BIP47 verfügen, wie z.B. PayNym auf Samourai Wallet oder Sparrow Wallet. Die Verknüpfung der Zahlungscodes der beiden Benutzer ermöglicht die Einrichtung eines geheimen Kanals zwischen ihnen. Um diesen Kanal ordnungsgemäß einzurichten, muss der Sender eine Transaktion auf der Bitcoin-Blockchain durchführen: die Benachrichtigungstransaktion (dazu komme ich später).

Die Verknüpfung der Zahlungscodes der beiden Benutzer erzeugt gemeinsame Geheimnisse, die wiederum eine große Anzahl von eindeutigen Bitcoin-Empfangsadressen generieren (genau 2^32). Tatsächlich wird die Zahlung mit BIP47 nicht an den Zahlungscode selbst gesendet, sondern an ganz normale Adressen, die aus den Zahlungscodes der Beteiligten abgeleitet werden.

Der Zahlungscode fungiert also als virtuelle Kennung, die aus dem Wallet-Schlüssel abgeleitet wird. In der HD-Wallet-Derivationsstruktur befindet sich der Zahlungscode in Tiefe 3, auf der Wallet-Kontoebene.

![image](assets/3.png)

Sein Ableitungszweck wird mit 47' (0x8000002F) in Bezug auf BIP47 angegeben. Ein Beispiel für einen Ableitungspfad für einen wiederverwendbaren Zahlungscode lautet:

> m/47'/0'/0'/

Damit Sie sich vorstellen können, wie ein Zahlungscode aussieht, hier ist meiner:

> PM8TJSBiQmNQDwTogMAbyqJe2PE2kQXjtgh88MRTxsrnHC8zpEtJ8j7Aj628oUFk8X6P5rJ7P5qDudE4Hwq9JXSRzGcZJbdJAjM9oVQ1UKU5j2nr7VR5

Dieser kann auch als QR-Code codiert werden, um die Kommunikation zu erleichtern:

![image](assets/4.png)

Was die PayNym Bots betrifft, diese Roboter, die man auf Twitter sieht, handelt es sich einfach um visuelle Darstellungen Ihres Zahlungscodes, die von Samourai Wallet erstellt werden. Sie werden durch eine Hash-Funktion erzeugt, was sie nahezu einzigartig macht. Hier ist meiner mit seiner Kennung:

> +throbbingpond8B1

![image](assets/5.png)

Diese Bots haben keine wirkliche technische Verwendung. Stattdessen erleichtern sie die Interaktion zwischen den Benutzern, indem sie eine virtuelle visuelle Identität schaffen.

Für den Benutzer ist der Prozess einer BIP47-Zahlung mit der PayNym-Implementierung äußerst einfach. Stellen wir uns vor, Alice möchte Zahlungen an Bob senden:

1. Bob verbreitet seinen QR-Code oder direkt seinen wiederverwendbaren Zahlungscode. Er kann ihn auf seiner Website, in seinen verschiedenen öffentlichen sozialen Netzwerken platzieren oder ihn über einen anderen Kommunikationsweg an Alice senden.
2. Alice öffnet ihre Samourai- oder Sparrow-Software und scannt oder fügt den Zahlungscode von Bob ein.
3. Alice verbindet ihren PayNym mit dem von Bob ("Follow" auf Englisch). Dieser Vorgang findet außerhalb der Blockchain statt und ist vollständig kostenlos.

4. Alice verbindet ihren PayNym mit dem von Bob ("Connect" auf Englisch). Dieser Vorgang findet "on chain" statt. Alice muss die Transaktions-Mining-Gebühren sowie eine feste Gebühr von 15.000 Sats für den Service auf Samourai bezahlen. Die Servicegebühren werden auf Sparrow angeboten. Dieser Schritt wird als Benachrichtigungstransaktion bezeichnet.

5. Sobald die Benachrichtigungstransaktion bestätigt ist, kann Alice eine BIP47-Zahlungstransaktion an Bob erstellen. Ihre Brieftasche generiert automatisch eine neue leere Empfangsadresse, für die nur Bob den privaten Schlüssel besitzt.

Die Durchführung der Benachrichtigungstransaktion, d.h. die Verbindung ihres PayNyms, ist ein obligatorischer Vorlauf, um BIP47-Zahlungen durchzuführen. Sobald dies jedoch erfolgt ist, kann der Absender mehrere Zahlungen an den Empfänger (genau 2^32) durchführen, ohne erneut eine Benachrichtigungstransaktion durchführen zu müssen.

Sie haben gesehen, dass es zwei verschiedene Operationen gibt, um PayNyms miteinander zu verbinden: verbinden und folgen. Die Verbindungsoperation ("connecter") entspricht der Benachrichtigungstransaktion von BIP47, die einfach eine Bitcoin-Transaktion mit bestimmten über eine OP_RETURN-Ausgabe übermittelten Informationen ist. Sie hilft dabei, eine verschlüsselte Kommunikation zwischen den beiden Benutzern herzustellen, um die erforderlichen gemeinsamen Geheimnisse zur Generierung neuer leerer Empfangsadressen zu erzeugen.

Die Verknüpfungsoperation ("follow" oder "relier") hingegen ermöglicht eine Verbindung auf Soroban, einem verschlüsselten Kommunikationsprotokoll auf Basis von Tor, das speziell von den Samourai-Teams entwickelt wurde.

Zusammenfassend:

- Das Verbinden von zwei PayNyms ("follow") ist völlig kostenlos. Dies hilft bei der Herstellung von verschlüsselten "off chain" -Kommunikationen, insbesondere zur Verwendung von Samourai-Kollaborationstransaktionstools (Stowaway oder StonewallX2). Diese Operation ist spezifisch für PayNym. Sie wird nicht im BIP47 beschrieben.

- Das Verbinden von zwei PayNyms ist kostenpflichtig. Dies beinhaltet die Durchführung der Benachrichtigungstransaktion, um die Verbindung herzustellen. Die Kosten umfassen mögliche Servicegebühren, Transaktions-Mining-Gebühren und 546 Sats, die an die Empfangsbenachrichtigungsadresse des Empfängers gesendet werden, um ihn über die Eröffnung des Tunnels zu informieren. Diese Operation ist mit BIP47 verbunden. Sobald sie durchgeführt wurde, kann der Absender mehrere BIP47-Zahlungen an den Empfänger durchführen.

Um zwei PayNyms verbinden zu können, müssen sie bereits miteinander verknüpft sein.

## Tutorials: Verwendung von PayNym.

Jetzt, da wir die Theorie gesehen haben, wollen wir uns gemeinsam die Praxis ansehen. Die Idee der untenstehenden Tutorials ist es, meinen PayNym in meiner Sparrow-Wallet mit meinem PayNym in meiner Samourai-Wallet zu verbinden. Das erste Tutorial zeigt Ihnen, wie Sie eine Transaktion mit dem wiederverwendbaren Zahlungscode von Samourai nach Sparrow durchführen können, und das zweite Tutorial beschreibt den gleichen Mechanismus von Sparrow nach Samourai.

> Ich habe diese Tutorials im Testnetz durchgeführt. Es handelt sich nicht um echte Bitcoins.

### Erstellen einer BIP47-Transaktion mit Samourai Wallet.

Um zu beginnen, benötigen Sie natürlich die Samourai Wallet-App. Sie können sie direkt aus dem Google Play Store herunterladen oder mit der APK-Datei, die auf der offiziellen Samourai-Website verfügbar ist.

Nachdem die Wallet initialisiert wurde, fordern Sie, falls noch nicht geschehen, Ihren PayNym an, indem Sie auf das Pluszeichen (+) unten rechts und dann auf "PayNym" klicken.

Der erste Schritt zur Durchführung einer BIP47-Zahlung besteht darin, den wiederverwendbaren Zahlungscode unseres Empfängers abzurufen. Anschließend können wir uns damit verbinden und uns dann verbinden:

![video](assets/6.mp4)

Nachdem die Benachrichtigungstransaktion bestätigt wurde, kann ich mehrere Zahlungen an meinen Empfänger senden. Jede Transaktion erfolgt automatisch mit einer neuen leeren Adresse, für die der Empfänger die Schlüssel besitzt. Dieser muss nichts tun, alles wird von meiner Seite aus berechnet.

So führen Sie eine BIP47-Transaktion in der Samourai Wallet durch:

![video](assets/7.mp4)

### Erstellen einer BIP47-Transaktion mit Sparrow Wallet.

Genau wie bei Samourai benötigen Sie natürlich die Sparrow-Software. Diese ist auf dem Computer verfügbar. Sie können sie von ihrer [offiziellen Website](https://sparrowwallet.com/) herunterladen.

Stellen Sie sicher, dass Sie die Signatur des Entwicklers und die Integrität der heruntergeladenen Software überprüfen, bevor Sie sie auf Ihrem Gerät installieren.

Erstellen Sie eine Wallet und fordern Sie Ihren PayNym an, indem Sie auf "Show PayNym" im Menü "Tool" in der oberen Leiste klicken:

![image](assets/8.png)

Anschließend müssen Sie Ihren PayNym mit dem PayNym Ihres Empfängers verbinden und verbinden. Geben Sie dazu seinen wiederverwendbaren Zahlungscode in das Fenster "Find Contact" ein, folgen Sie ihm und führen Sie dann die Benachrichtigungstransaktion durch, indem Sie auf "Link Contact" klicken:

![image](assets/9.png)

Nachdem die Benachrichtigungstransaktion bestätigt wurde, können Zahlungen an den wiederverwendbaren Zahlungscode gesendet werden. Hier ist der Ablauf:

![video](assets/10.mp4)

Jetzt, da wir den praktischen Aspekt der PayNym-Implementierung von BIP47 untersucht haben, wollen wir uns gemeinsam ansehen, wie all diese Mechanismen funktionieren und welche kryptographischen Methoden verwendet werden.

## Die Mechanismen von BIP47.

Um die Mechanismen von BIP47 zu studieren, ist es wichtig, die Struktur der hierarchisch deterministischen (HD) Wallet, die Mechanismen zur Ableitung von Kinderschlüsselpaaren und die Prinzipien der elliptischen Kurvenkryptographie zu verstehen. Glücklicherweise finden Sie auf meinem Blog alle Informationen, die für das Verständnis dieses Teils erforderlich sind:

- [Verständnis der Ableitungspfade einer Bitcoin Wallet](https://www.pandul.fr/post/comprendre-les-chemins-de-d%C3%A9rivation-d-un-portefeuille-bitcoin)

- [Die Bitcoin Wallet - Auszug aus dem eBook Bitcoin Démocratisé 2](https://www.pandul.fr/post/le-portefeuille-bitcoin-extrait-ebook-bitcoin-d%C3%A9mocratis%C3%A9-2)

### Der wiederverwendbare Zahlungscode.

Wie in Teil zwei dieses Papiers erklärt, befindet sich der wiederverwendbare Zahlungscode in der Tiefe drei der HD Wallet. Er ist letztendlich in seiner Platzierung, Struktur und Funktion einer xpub ähnlich.

Hier sind die verschiedenen Teile, aus denen ein 80-Byte-Zahlungscode besteht:

- Byte 0: Die Version. Wenn die erste Version von BIP47 verwendet wird, ist dieses Byte gleich 0x01.

- Byte 1: Das Bitfeld. Dieser Raum ist reserviert, um zusätzliche Informationen für spezifische Verwendungen anzugeben. Wenn nur PayNym verwendet wird, ist dieses Byte gleich 0x00.

- Byte 2: Die Parität von y. Dieses Byte gibt 0x02 oder 0x03 an, abhängig von der Parität (gerade oder ungerade Anzahl) des Werts der y-Koordinate unseres öffentlichen Schlüssels. Für weitere Informationen zu dieser Praxis lesen Sie bitte Schritt 1 des Abschnitts "Adressableitung" in diesem Artikel.

- Von Byte 3 bis Byte 34: Der Wert von x. Diese Bytes geben die x-Koordinate unseres öffentlichen Schlüssels an. Die Konkatenation von x und der Parität von y ergibt unseren komprimierten öffentlichen Schlüssel.

- Von Byte 35 bis Byte 66: Der Chain-Code. Dieser Raum ist für den mit dem oben genannten öffentlichen Schlüssel verbundenen Chain-Code reserviert.

- Von Byte 67 bis Byte 79: Die Polsterung. Dieser Raum ist für mögliche zukünftige Entwicklungen reserviert. Für Version 1 füllen wir ihn einfach mit Nullen, um die Daten auf 80 Bytes, die Größe der OP_RETURN-Ausgabedaten, aufzufüllen.

Hier ist die hexadezimale Darstellung meines wiederverwendbaren Zahlungscodes aus dem vorherigen Teil, mit den Farben, die den oben genannten Bytes entsprechen:
'>0x010002a0716529bae6b36c5c9aa518a52f9c828b46ad8d907747f0d09dcd4d9a39e97c3c5f37c470c390d842f364086362f6122f412e2b0c7e7fc6e32287e364a7a36a00000000000000000000000000

Anschließend muss das Präfixbyte "P" hinzugefügt werden, um auf den ersten Blick zu erkennen, dass es sich um einen Zahlungscode handelt. Dieses Byte ist 0x47.

> 0x47010002a0716529bae6b36c5c9aa518a52f9c828b46ad8d907747f0d09dcd4d9a39e97c3c5f37c470c390d842f364086362f6122f412e2b0c7e7fc6e32287e364a7a36a00000000000000000000000000

Schließlich berechnen wir die Prüfsumme dieses Zahlungscodes mit HASH256, also einer doppelten Hashfunktion mit der SHA256-Funktion. Wir nehmen die ersten vier Bytes dieses Hashwertes und fügen sie am Ende hinzu (in rosa).

> 0x47010002a0716529bae6b36c5c9aa518a52f9c828b46ad8d907747f0d09dcd4d9a39e97c3c5f37c470c390d842f364086362f6122f412e2b0c7e7fc6e32287e364a7a36a00000000000000000000000000567080c4

Der Zahlungscode ist bereit und muss nur noch in Base 58 umgewandelt werden:

> PM8TJSBiQmNQDwTogMAbyqJe2PE2kQXjtgh88MRTxsrnHC8zpEtJ8j7Aj628oUFk8X6P5rJ7P5qDudE4Hwq9JXSRzGcZJbdJAjM9oVQ1UKU5j2nr7VR5

Wie Sie sehen können, ähnelt diese Konstruktion stark der Struktur eines erweiterten öffentlichen Schlüssels vom Typ "xpub".

Während dieses Prozesses zur Erstellung unseres Zahlungscodes haben wir einen komprimierten öffentlichen Schlüssel und einen Chain-Code verwendet. Diese beiden Elemente sind das Ergebnis einer deterministischen und hierarchischen Ableitung von der Wallet-Seed, indem wir dem folgenden Ableitungspfad folgen: m/47'/0'/0'/.'
Concrètement, pour obtenir la clé publique et le code de chaîne du code de paiement réutilisable, on va calculer la clé privée maîtresse depuis la graine, puis dériver une paire fille avec l'index 47 + 2^31 (dérivation renforcée). Ensuite, on dérive deux fois des paires filles avec l'index 2^31 (dérivation renforcée).

> Si vous souhaitez en savoir plus sur la dérivation de paires de clés filles au sein d'un portefeuille déterministe hiérarchique Bitcoin, je vous conseille de faire CRYPTO301

### La méthode cryptographique : l'échange de clés Diffie-Hellman établi sur les courbes elliptiques (ECDH).

La méthode cryptographique utilisée à la base du BIP47 est ECDH (Elliptic-Curve Diffie-Hellman = Échange de clés Diffie-Hellman établi sur les courbes elliptiques). Ce protocole est une variante de l'échange de clés Diffie-Hellman classique.

Diffie-Hellman, dans sa première version, est un protocole d'accord de clés présenté en 1976 qui permet à deux personnes, à partir de deux paires (clés publiques et clés privées), de déterminer un secret partagé en échangeant sur un canal de communication non sécurisé.

![image](assets/11.png)

Ce secret partagé (la clé rouge) peut ensuite être utilisé pour réaliser d'autres tâches. Typiquement, on peut utiliser ce secret partagé pour chiffrer et déchiffrer une communication sur un réseau non sécurisé :

![image](assets/12.png)

Pour réussir cet échange, Diffie-Hellman utilise l'arithmétique modulaire afin de calculer le secret commun. Voici son fonctionnement vulgarisé :

- Alice et Bob déterminent une couleur commune, ici le jaune. Cette couleur est connue de tous. C'est une donnée publique.

- Alice choisi une couleur secrète, ici le rouge. Elle mélange les deux couleurs ce qui lui donne de l'orange.

- Bob choisi une couleur secrète, ici le bleu canard. Il mélange les deux couleurs ce qui lui donne du bleu ciel.

- Alice et Bob peuvent s'échanger les couleurs obtenues : l'orange et le bleu ciel. Cet échange peut se faire sur un réseau non sécurisé et observé par des attaquants.

- Alice mélange la couleur bleu ciel reçue de Bob avec sa couleur secrète (rouge). Elle obtient du marron.

- Bob mélange la couleur orange reçue d'Alice avec sa couleur secrète (bleu canard). Il obtient cette même couleur marron.

![image](assets/13.png)

> Crédit : Idée originale : A.J. Han VinckVersion vectorielle : FlugaalTraduction : Dereckson, Public domain, via Wikimedia Commons. https://commons.wikimedia.org/wiki/File:Diffie-Hellman_Key_Exchange_(fr).svg
> 'Dans dieser Vereinfachung repräsentiert die braune Farbe das Geheimnis, das zwischen Alice und Bob geteilt wird. Man muss sich vorstellen, dass es in Wirklichkeit für den Angreifer unmöglich ist, die orangefarbene und hellblaue Farbe zu trennen, um die geheimen Farben von Alice oder Bob wiederherzustellen.
> Nun betrachten wir seine tatsächliche Funktionsweise. Auf den ersten Blick scheint Diffie-Hellman schwer zu verstehen zu sein. In Wirklichkeit ist das Funktionsprinzip jedoch fast kinderleicht. Bevor ich Ihnen die Mechanismen im Detail erkläre, möchte ich Ihnen kurz zwei mathematische Konzepte in Erinnerung rufen, die wir benötigen werden (und die übrigens auch in vielen anderen kryptographischen Methoden verwendet werden).

1. Eine Primzahl ist eine natürliche Zahl, die nur zwei Teiler hat: 1 und sich selbst. Zum Beispiel ist die Zahl 7 eine Primzahl, da sie nur durch 1 und 7 (sich selbst) teilbar ist. Die Zahl 8 hingegen ist keine Primzahl, da sie durch 1, 2, 4 und 8 teilbar ist. Sie hat also nicht nur zwei, sondern vier ganze und positive Teiler.

2. Das "Modulo" (notiert als "mod" oder "%") ist eine mathematische Operation, bei der der Rest der euklidischen Division der ersten Zahl durch die zweite Zahl zurückgegeben wird. Zum Beispiel ist 16 mod 5 gleich 1.

Der Diffie-Hellman-Schlüsselaustausch zwischen Alice und Bob funktioniert wie folgt:

- Alice und Bob wählen zwei gemeinsame Zahlen: p und g. p ist eine Primzahl. Je größer diese Zahl p ist, desto sicherer wird Diffie-Hellman sein. g ist eine primitive Wurzel von p. Diese beiden Zahlen können unverschlüsselt über ein unsicheres Netzwerk kommuniziert werden, sie entsprechen der gelben Farbe in der obigen Vereinfachung. Alice und Bob müssen einfach genau die gleichen Werte für p und g haben.

- Nachdem die Parameter festgelegt wurden, wählen Alice und Bob jeweils eine geheime Zufallszahl. Die von Alice erhaltene Zufallszahl wird als a bezeichnet (entspricht der roten Farbe) und die von Bob erhaltene Zufallszahl wird als b bezeichnet (entspricht der türkisblauen Farbe). Diese beiden Zahlen müssen geheim bleiben.

- Anstatt diese Zahlen a und b auszutauschen, berechnet jede Partei A (großgeschrieben) und B (großgeschrieben) wie folgt:

> A ist gleich g hoch a modulo p:
> A = g^a % p

> B ist gleich g hoch b modulo p:
> B = g^b % p

- Diese Zahlen A (entspricht der orangefarbenen Farbe) und B (entspricht der hellblauen Farbe) werden zwischen den beiden Parteien ausgetauscht. Der Austausch kann unverschlüsselt über ein unsicheres Netzwerk erfolgen.

- Alice, die nun B kennt, berechnet den Wert von z wie folgt:

> z ist gleich B hoch a modulo p:
> z = B^a % p'

- Zur Erinnerung, B = g^b % p. Also haben wir:

  > z = B^a % p
  > z = (g^b)^a % p
  >
  > Gemäß den Rechenregeln für Potenzen:
  >
  > (x^n)^m = x^nm
  >
  > Also haben wir:
  >
  > z = g^ba % p

- Bob, der jetzt A kennt, wird auch den Wert von z berechnen:
  > z ist gleich A hoch b modulo p:
  >
  > z = A^b % p
  >
  > Also haben wir:
  >
  > z = (g^a)^b % p
  > z = g^ab % p
  > z = g^ba % p

Dank der Distributivität des Modulo-Operators finden Alice und Bob genau den gleichen Wert für z. Diese Zahl repräsentiert ihr gemeinsames Geheimnis, das Äquivalent zur Farbe Braun in der vorherigen Veranschaulichung. Sie können dieses gemeinsame Geheimnis verwenden, um eine Kommunikation zwischen ihnen auf einem unsicheren Netzwerk zu verschlüsseln.

![Schema der technischen Funktionsweise von Diffie-Hellman](assets/14.png)

Ein Angreifer, der im Besitz von p, g, A und B ist, wird nicht in der Lage sein, a, b oder z zu berechnen. Eine solche Operation würde einer Umkehrung der Exponentiation entsprechen. Diese Berechnung ist unmöglich, außer man versucht alle Möglichkeiten einzeln auszuprobieren, da wir mit einem endlichen Körper arbeiten. Dies würde bedeuten, das diskrete Logarithmusproblem zu lösen, also das Inverse der Exponentialfunktion in einer endlichen zyklischen Gruppe zu berechnen.

Solange wir also ausreichend große Werte für a, b und p wählen, ist Diffie-Hellman sicher. Typischerweise wird mit Parametern von 2.048 Bits (eine Zahl mit 600 Dezimalstellen) das Ausprobieren aller Möglichkeiten für a und b illusorisch sein. Mit solchen Größenordnungen gilt der Algorithmus heute als sicher.

Genau hier liegt jedoch der Hauptnachteil des Diffie-Hellman-Protokolls. Um sicher zu sein, muss der Algorithmus große Zahlen verwenden. Daher bevorzugt man heute den Einsatz des ECDH-Algorithmus, einer Variante von Diffie-Hellman, der eine elliptische Kurve verwendet. Dadurch können wir mit viel kleineren Zahlen arbeiten und dennoch ein gleichwertiges Sicherheitsniveau beibehalten, was die Ressourcen für Berechnung und Speicherung reduziert.

Das allgemeine Prinzip des Algorithmus bleibt jedoch dasselbe. Anstelle einer zufälligen Zahl a und einer aus a berechneten Zahl A mit modularer Exponentiation verwenden wir ein Schlüsselpaar, das auf einer elliptischen Kurve etabliert ist. Anstelle der Distributivität des Modulo-Operators verwenden wir hier das Gruppenrecht auf elliptischen Kurven, genauer gesagt die Assoziativität dieses Gesetzes.

> Wenn Sie keine Kenntnisse über die Funktionsweise von privaten und öffentlichen Schlüsseln auf einer elliptischen Kurve haben, erkläre ich Ihnen die Grundlagen dieser Methode in den ersten sechs Teilen dieses Artikels.

Um es grob zusammenzufassen, ist ein privater Schlüssel eine zufällige Zahl zwischen 1 und n-1 (wobei n die Ordnung der Kurve ist), und ein öffentlicher Schlüssel ist ein eindeutiger Punkt auf der Kurve, der durch Addition und Verdoppelung von Punkten vom Generatorpunkt aus bestimmt wird, wie folgt:

> K = k·G

Dabei ist K der öffentliche Schlüssel, k ist der private Schlüssel und G ist der Generatorpunkt.

Eine Eigenschaft dieses Schlüsselpaares ist, dass es sehr einfach ist, K zu bestimmen, wenn man k und G kennt, aber es ist heute unmöglich, k zu bestimmen, wenn man K und G kennt. Es handelt sich um eine Einwegfunktion.

Mit anderen Worten, man kann den öffentlichen Schlüssel leicht berechnen, wenn man den privaten Schlüssel kennt, aber es ist unmöglich, den privaten Schlüssel zu berechnen, wenn man den öffentlichen Schlüssel kennt. Diese Sicherheit beruht erneut auf der Unmöglichkeit der Berechnung des diskreten Logarithmus.

Wir werden diese Eigenschaft nutzen, um unseren Diffie-Hellman-Algorithmus anzupassen. Der Arbeitsablauf von ECDH ist wie folgt:

- Alice und Bob einigen sich auf eine kryptographisch sichere elliptische Kurve und deren Parameter. Diese Informationen sind öffentlich.

- Alice generiert eine zufällige Zahl ka, die ihr privater Schlüssel sein wird. Dieser private Schlüssel muss geheim bleiben. Sie bestimmt ihren öffentlichen Schlüssel Ka durch Addition und Verdoppelung von Punkten auf der gewählten elliptischen Kurve.

> Ka = ka·G

- Bob generiert ebenfalls eine zufällige Zahl, die sein privater Schlüssel kb sein wird. Und er berechnet den zugehörigen öffentlichen Schlüssel Kb.

> Kb = kb·G

- Alice und Bob tauschen ihre öffentlichen Schlüssel Ka und Kb über ein unsicheres öffentliches Netzwerk aus.

- Alice berechnet einen Punkt (x,y) auf der Kurve, indem sie ihren privaten Schlüssel ka auf den öffentlichen Schlüssel von Bob Kb anwendet.

> (x,y) = ka·Kb

- Bob berechnet einen Punkt (x,y) auf der Kurve, indem er seinen privaten Schlüssel kb auf den öffentlichen Schlüssel von Alice Ka anwendet.

> (x,y) = kb·Ka

- Alice und Bob erhalten den gleichen Punkt auf der elliptischen Kurve. Das gemeinsame Geheimnis wird die x-Koordinate dieses Punktes sein.

Sie erhalten das gleiche gemeinsame Geheimnis, weil:

> (x,y) = ka·Kb = ka·kb·G = kb·ka·G = kb·Ka

Ein potenzieller Angreifer, der das unsichere öffentliche Netzwerk beobachtet, kann nur die öffentlichen Schlüssel von jedem und die Parameter der gewählten Kurve erhalten. Wie zuvor erklärt, reichen diese beiden Informationen allein nicht aus, um die privaten Schlüssel zu bestimmen, und daher kann der Angreifer nicht auf das Geheimnis zugreifen.
'ECDH ist ein Algorithmus, der einen Schlüsselaustausch ermöglicht. Es wird oft zusammen mit anderen kryptographischen Methoden verwendet, um ein Protokoll zu definieren. Zum Beispiel wird ECDH im Herzen von TLS (Transport Layer Security) verwendet, einem Verschlüsselungs- und Authentifizierungsprotokoll, das für die Transportebene des Internets verwendet wird. TLS verwendet ECDHE für den Schlüsselaustausch, eine Variante von ECDH, bei der die Schlüssel ephemeral sind, um anhaltende Vertraulichkeit zu gewährleisten. Neben ECDHE verwendet TLS auch einen Authentifizierungsalgorithmus wie ECDSA, eine Verschlüsselungsalgorithmus wie AES und eine Hash-Funktion wie SHA256.
TLS definiert unter anderem das "s" in "https" sowie das kleine Schlosssymbol, das Sie oben links in Ihrem Webbrowser sehen, um eine verschlüsselte Kommunikation zu gewährleisten. Sie verwenden also ECDH, während Sie diesen Artikel lesen, und verwenden es wahrscheinlich täglich, ohne es zu bemerken.

### Die Benachrichtigungstransaktion.

Wie wir im vorherigen Abschnitt entdeckt haben, ist ECDH eine Variante des Diffie-Hellman-Austauschs, bei dem Schlüsselpaare auf einer elliptischen Kurve erstellt werden. Das passt gut, denn wir haben viele Schlüsselpaare, die diesem Standard entsprechen, in unseren Bitcoin-Hierarchical-Deterministic-Wallets!

Die Idee besteht also darin, die Schlüsselpaare der hierarchischen deterministischen Bitcoin-Wallets beider Parteien zu verwenden, um gemeinsame und ephemere Geheimnisse zwischen ihnen zu etablieren. Innerhalb von BIP47 wird daher eher ECDHE (Elliptic Curve Diffie-Hellman Ephemeral) verwendet.

ECDHE wird im BIP47 zum ersten Mal verwendet, um den Zahlungscode vom Absender an den Empfänger zu übertragen. Dies ist die berühmte Benachrichtigungstransaktion. Damit BIP47 verwendet werden kann, müssen beide Parteien (der Absender, der Zahlungen sendet, und der Empfänger, der Zahlungen empfängt) den Zahlungscode der anderen Partei kennen. Dies ist erforderlich, um die ephemeren öffentlichen Schlüssel abzuleiten und somit dedizierte Empfangsadressen zu generieren.

Vor diesem Austausch kennt der Absender logischerweise bereits den Zahlungscode des Empfängers, da er ihn off-chain erhalten hat, zum Beispiel auf seiner Website oder in sozialen Netzwerken. Der Empfänger kennt jedoch möglicherweise nicht den Zahlungscode des Absenders. Es muss ihm also übermittelt werden, sonst kann er seine ephemeren Schlüssel nicht ableiten und somit nicht wissen, wo sich seine Bitcoins befinden und seine Mittel nicht freigeben. Man könnte es ihm off-chain übermitteln, mit einem anderen Kommunikationssystem, aber das würde ein Problem darstellen, wenn die Wallet aus dem Seed wiederhergestellt wird.'
En effet, comme je l'ai déjà évoqué, les adresses BIP47 ne sont pas dérivées depuis la graine du destinataire (sinon autant utiliser une de ses xpub directement), mais sont le fruit d'un calcul impliquant les deux codes de paiement : celui du destinataire et celui de l'expéditeur. C’est pourquoi, si le destinataire perd son portefeuille et essaie de le récupérer depuis sa graine, il devra nécessairement disposer de tous les codes de paiement des personnes qui lui ont envoyé des bitcoins via BIP47.
On pourrait donc facilement utiliser le BIP47 sans cette transaction de notification, mais il faudrait que chaque utilisateur fasse une sauvegarde des codes de paiement de ses pairs. Cette situation restera ingérable tant que l'on n'aura pas trouvé un moyen simple et résilient de réaliser, de stocker et de tenir à jour ces sauvegardes. La transaction de notification est donc quasiment obligatoire dans l'état actuel des choses.

En plus de ce rôle de sauvegarde des codes de paiement, comme son nom l'indique, cette transaction joue également un rôle de notification du destinataire. Elle permet de signaler à son client qu'un tunnel vient d'être ouvert.

Avant de vous expliquer plus en détail le fonctionnement technique de la transaction de notification, je souhaite vous parler un peu de modèle de confidentialité. En effet, celui du BIP47 va justifier certaines précautions prises lors de la construction de cette transaction initiale.

Le code de paiement en lui-même ne constitue pas directement un risque de perte de confidentialité. Contrairement au modèle classique de Bitcoin qui permet de casser le flux d'information entre l'identité de l'utilisateur et les transactions, notamment en gardant les clés publiques anonymes, le code de paiement peut être associé directement à une identité. Ce n'est évidemment pas une obligation, mais ce lien n'est pas dangereux.

En effet, le code de paiement ne dérive pas directement les adresses utilisées pour recevoir des paiements BIP47. Au lieu de cela, les adresses sont obtenues en appliquant ECDHE entre des clés filles des codes de paiements des deux parties.

Un code de paiement seul ne constitue donc pas un risque direct de perte de confidentialité puisque l'on ne dérive que l'adresse de notification depuis celui-ci. On peut en tirer certaines informations, mais on ne pourra normalement pas savoir avec qui vous faites des transactions.

Il est donc essentiel de maintenir cette séparation stricte entre les codes de paiements des utilisateurs. Dans cet objectif, l'étape de communication initiale du code est un moment critique pour la confidentialité du paiement, et pourtant obligatoire pour le bon fonctionnement du protocole. Si un des deux codes de paiements peut être récupéré publiquement (par exemple, sur un site web), le second code, c'est-à-dire celui de l'envoyeur, ne doit pas être associé au premier.

Par exemple, imaginons que je souhaite faire un don avec BIP47 à un mouvement de protestation pacifique au Canada:

- Diese Organisation hat ihren Zahlungscode direkt auf ihrer Website oder in ihren sozialen Netzwerken veröffentlicht.
- Dieser Code ist also mit der Bewegung verbunden.

- Ich hole mir diesen Zahlungscode.

- Bevor ich ihnen eine Transaktion senden kann, muss ich sicherstellen, dass sie von meinem persönlichen Zahlungscode wissen, der auch mit meiner Identität verbunden ist, da ich ihn zum Empfangen von Transaktionen aus meinen sozialen Netzwerken verwende.

Wie kann ich ihn ihnen übermitteln? Wenn ich ihn mit einem herkömmlichen Kommunikationsmittel sende, besteht die Gefahr, dass die Informationen durchsickern und ich als Person, die friedliche Bewegungen unterstützt, erfasst werde.

Die Benachrichtigungstransaktion ist sicherlich nicht die einzige Lösung, um den Zahlungscode des Absenders geheim zu übermitteln, erfüllt jedoch derzeit perfekt diese Rolle, indem sie mehrere Sicherheitsebenen anwendet.

Im folgenden Schema stellen die roten Linien den Zeitpunkt dar, an dem der Informationsfluss unterbrochen werden muss, und die schwarzen Pfeile stellen die unbestreitbaren Verbindungen dar, die von einem externen Beobachter hergestellt werden können:

![Schema des Modells für die Vertraulichkeit des wiederverwendbaren Zahlungscodes](assets/15.png)

In der Realität ist es für das klassische Bitcoin-Vertraulichkeitsmodell oft schwierig, den Informationsfluss zwischen dem Schlüsselpaar und dem Benutzer vollständig zu unterbrechen, insbesondere bei Ferntransaktionen. Zum Beispiel muss der Empfänger in einer Spendenkampagne eine Adresse oder einen öffentlichen Schlüssel auf seiner Website oder in seinen sozialen Netzwerken preisgeben. Die ordnungsgemäße Verwendung von BIP47, d.h. mit der Benachrichtigungstransaktion, löst dieses Problem durch ECDHE und die Verschlüsselungsschicht, die wir untersuchen werden.

Natürlich wird das klassische Bitcoin-Vertraulichkeitsmodell immer noch auf der Ebene der ephemeren öffentlichen Schlüssel beobachtet, die aus der Verknüpfung der beiden Zahlungscodes abgeleitet werden. Die beiden Modelle sind voneinander abhängig. Ich möchte hier nur darauf hinweisen, dass im Gegensatz zur herkömmlichen Verwendung eines öffentlichen Schlüssels zum Empfangen von Bitcoins der Zahlungscode mit einer Identität verbunden sein kann, da die Information "Bob führt eine Transaktion mit Alice durch" zu einem anderen Zeitpunkt unterbrochen wird. Der Zahlungscode wird verwendet, um Zahlungsadressen zu generieren, aber durch bloße Beobachtung der Blockchain ist es unmöglich, eine BIP47-Zahlungstransaktion den verwendeten Zahlungscodes zuzuordnen.

### Aufbau der Benachrichtigungstransaktion.

Lassen Sie uns nun sehen, wie diese Benachrichtigungstransaktion funktioniert. Stellen wir uns vor, Alice möchte mit BIP47 Geld an Bob senden. In meinem Beispiel fungiert Alice als Absender und Bob als Empfänger. Letzterer hat seinen Zahlungscode auf seiner Website veröffentlicht. Alice kennt also bereits Bobs Zahlungscode.

1. Alice berechnet ein gemeinsames Geheimnis mit ECDH: '

- Sie wählt einen Schlüssel aus ihrer HD-Brieftasche aus, der sich auf einem anderen Zweig als ihr Zahlungscode befindet. Achtung, dieser Schlüssel darf nicht leicht mit Alice' Benachrichtigungsadresse oder Identität in Verbindung gebracht werden (siehe vorheriger Abschnitt).
- Alice wählt den privaten Schlüssel dieses Paares aus. Wir nennen ihn "a" (kleingeschrieben).

> a

- Alice erhält den öffentlichen Schlüssel, der mit Bobs Benachrichtigungsadresse verknüpft ist. Dieser Schlüssel ist das erste abgeleitete Kind vom Zahlungscode von Bob (Index 0). Wir nennen diesen öffentlichen Schlüssel "B" (großgeschrieben). Der private Schlüssel, der mit diesem öffentlichen Schlüssel verknüpft ist, wird "b" genannt (kleingeschrieben). "B" wird durch Addition und Verdoppelung von Punkten auf der elliptischen Kurve von "G" (dem Generatorpunkt) mit "b" (dem privaten Schlüssel) bestimmt.

> B = b·G

- Alice berechnet einen geheimen Punkt "S" (großgeschrieben) auf der elliptischen Kurve, indem sie ihren privaten Schlüssel "a" auf den öffentlichen Schlüssel von Bob "B" anwendet.

> S = a·B

- Alice berechnet den Verblindungsfaktor "f", der verwendet wird, um ihren Zahlungscode zu verschlüsseln. Dazu generiert sie eine pseudozufällige Zahl mit der HMAC-SHA512-Funktion. Als zweiten Eingabewert für diese Funktion verwendet sie einen Wert, den nur Bob wiederfinden kann: (x), die Abszisse des zuvor berechneten geheimen Punktes. Der erste Eingabewert ist (o), das UTXO, das als Eingabe für diese Transaktion verwendet wird (Outpoint).

> f = HMAC-SHA512(o, x)

2. Alice konvertiert ihren persönlichen Zahlungscode in Binärformat.

3. Sie verwendet diesen Verblindungsfaktor als Schlüssel, um eine symmetrische Verschlüsselung auf den Payload ihres Zahlungscodes anzuwenden. Der verwendete Verschlüsselungsalgorithmus ist ein einfaches XOR. Die durchgeführte Operation ist vergleichbar mit dem Vernam-Chiffre, auch bekannt als "One-Time Pad":

- Alice teilt zunächst ihren Verblindungsfaktor in zwei Teile auf: Die ersten 32 Bytes werden als "f1" bezeichnet und die letzten 32 Bytes als "f2". Es gilt also:

> f = f1 || f2

- Alice berechnet separat das verschlüsselte (x') der Abszisse des öffentlichen Schlüssels (x) ihres Zahlungscodes und das verschlüsselte (c') ihres Kettencodes (c). "f1" und "f2" fungieren jeweils als Verschlüsselungsschlüssel. Die verwendete Operation ist das XOR (exklusives Oder).

> x' = x XOR f1
>
> c>' = c XOR f2'
> '\* Alice ersetzt die echten Werte der x-Koordinate des öffentlichen Schlüssels und des Chaincodes (c) in ihrem Zahlungscode durch die verschlüsselten Werte (x') und (c').

Bevor wir die technische Beschreibung dieser Benachrichtigungstransaktion fortsetzen, wollen wir uns einen Moment mit der XOR-Operation befassen. XOR ist ein bitweiser logischer Operator, der auf der Booleschen Algebra basiert. Aus zwei Bit-Operanden gibt er 1 zurück, wenn die Bits gleicher Rangordnung unterschiedlich sind, und er gibt 0 zurück, wenn die Bits gleicher Rangordnung gleich sind. Hier ist die Wahrheitstabelle für XOR in Abhängigkeit von den Werten der Operanden D und E:

| D   | E   | D XOR E |
| --- | --- | ------- |
| 0   | 0   | 0       |
| 0   | 1   | 1       |
| 1   | 0   | 1       |
| 1   | 1   | 0       |

Zum Beispiel:

> 0110 XOR 1110 = 1000

Oder auch:

> 010011 XOR 110110 = 100101

Bei der Verwendung von ECDH ist die Verwendung von XOR als Verschlüsselungsschicht besonders sinnvoll. Erstens ist die Verschlüsselung dank dieses Operators symmetrisch. Dadurch kann der Empfänger den Zahlungscode mit demselben Schlüssel entschlüsseln, der zur Verschlüsselung verwendet wurde. Der Verschlüsselungs- und Entschlüsselungsschlüssel wird aus dem gemeinsamen Geheimnis durch ECDH berechnet.

Diese Symmetrie wird durch die Eigenschaften der Kommutativität und Assoziativität des XOR-Operators ermöglicht:

- Weitere Eigenschaften:
  -> D ⊕ D = 0
  -> D ⊕ 0 = D

- Kommutativität:
  D ⊕ E = E ⊕ D

- Assoziativität:
  D ⊕ (E ⊕ Z) = (D ⊕ E) ⊕ Z = D ⊕ E ⊕ Z

- Symmetrie:
  Wenn: D ⊕ E = L
  Dann: D ⊕ L = D ⊕ (D ⊕ E) = D ⊕ D ⊕ E = 0 ⊕ E = E
  -> D ⊕ L = E
  '''''
  Ensuite, cette méthode de chiffrement ressemble beaucoup au chiffre de Vernam (One-Time Pad), le seul algorithme de chiffrement connu à ce jour qui dispose d'une sécurité inconditionnelle (ou absolue). Pour que le chiffre de Vernam dispose de cette caractéristique, il faut que la clé de chiffrement soit parfaitement aléatoire, qu'elle soit de même taille que le message et qu'elle ne soit utilisée qu'une seule fois. Dans la méthode de chiffrement utilisée ici pour le BIP47, la clé est bien de la même taille que le message, le facteur aveuglant fait exactement la même taille que la concaténation de l'abscisse de la clé publique avec le code de chaine du code de paiement. Cette clé de chiffrement est bien utilisée une seule fois. En revanche, cette clé n'est pas issue d'un parfait aléa puisqu'elle est un HMAC. Elle est plutôt pseudo-aléatoire. Ce n'est donc pas un chiffre de Vernam, mais la méthode s'en rapproche.

Revenons à notre construction de la transaction de notification :

4. Alice dispose donc actuellement de son code de paiement avec une charge utile chiffrée. Elle va construire et diffuser une transaction impliquant sa clé publique "A" en input, un output à destination de l'adresse de notification de Bob, et une sortie OP_RETURN constituée de son code de paiement avec la charge utile chiffrée. Cette transaction est la transaction de notification.

l'OP_RETURN est un Opcode, c'est-à-dire un script, qui permet de marquer une sortie de transaction Bitcoin comme invalide. Aujourd'hui, il est utilisé pour diffuser ou pour ancrer de l'information sur la blockchain Bitcoin. On peut y stocker jusqu'à 80 octets de datas qui sont inscrites sur la chaine, et donc visibles par tous les autres utilisateurs.

Comme nous l'avons vu dans la partie précédente, Diffie-Hellman est utilisé pour générer un secret partagé entre deux utilisateurs qui communiquent sur un réseau non sécurisé, et potentiellement observé par des attaquants. Dans le BIP47, ECDH est utilisé pour pouvoir communiquer sur le réseau Bitcoin, qui par nature est un réseau de communication transparent et observé par de nombreux attaquants. Le secret partagé calculé grâce à l'échange de clés Diffie-Hellman sur la courbe elliptique est ensuite utilisé pour chiffrer l'information secrète à transmettre : le code de paiement de l'expéditeur (Alice).

Voici un schéma extrait du BIP47 qui illustre ce que l'on vient de décrire :

![Schéma Alice envoie son code de paiement masqué à l'adresse de notification de Bob](assets/16.png)

Crédit : Reusable Payment Codes for Hierarchical Deterministic Wallets, Justus Ranvier. https://github.com/bitcoin/bips/blob/master/bip-0047.mediawiki

Si l'on fait correspondre ce schéma avec ce que je vous ai décris précédemment :

- "Wallet Priv-Key" du côté d'Alice correspond à : a.

- "Child Pub-Key 0" du côté de Bob correspond à : B.
- "Notification Shared Secret" entspricht: f.
- "Masked Payment Code" entspricht dem maskierten Zahlungscode, d.h. mit verschlüsselten Nutzdaten: x' und c'.

- "Notification Transaction" ist die Transaktion, die den OP_RETURN enthält.

Ich werde die Schritte zusammenfassen, die wir gerade besprochen haben, um eine Benachrichtigungstransaktion durchzuführen:

- Alice erhält den Zahlungscode und die Benachrichtigungsadresse von Bob.

- Alice wählt eine UTXO aus ihrem HD-Wallet mit dem entsprechenden Schlüsselpaar aus.

- Sie berechnet einen geheimen Punkt auf der elliptischen Kurve mit ECDH.

- Sie verwendet diesen geheimen Punkt, um einen HMAC zu berechnen, der als Blindfaktor dient.

- Sie verwendet diesen Blindfaktor, um die Nutzdaten ihres persönlichen Zahlungscodes zu verschlüsseln.

- Sie verwendet eine OP_RETURN-Transaktionsausgabe, um den maskierten Zahlungscode an Bob zu übertragen.

Um das Funktionieren genauer zu verstehen, insbesondere die Verwendung von OP_RETURN, betrachten wir gemeinsam eine echte Benachrichtigungstransaktion. Ich habe eine solche Transaktion im Testnet durchgeführt, die Sie hier finden können:

https://mempool.space/fr/testnet/tx/0e2e4695a3c49272ef631426a9fd2dae6ec3a469e3a39a3db51aa476cd09de2e

TXID:

> 0e2e4695a3c49272ef631426a9fd2dae6ec3a469e3a39a3db51aa476cd09de2e

![Benachrichtigungstransaktion BIP47](assets/17.png)

Credit: https://blockstream.info/

Beim Betrachten dieser Transaktion können wir bereits sehen, dass sie eine einzige Eingabe und 4 Ausgaben hat:

- Die erste Ausgabe ist OP_RETURN, die meinen maskierten Zahlungscode enthält.

- Die zweite Ausgabe von 546 Sats zeigt auf die Benachrichtigungsadresse meines Empfängers.

- Die dritte Ausgabe von 15.000 Sats sind die Servicegebühren, da ich Samourai Wallet für den Aufbau dieser Transaktion verwendet habe.

- Die vierte Ausgabe von zwei Millionen Sats ist das Wechselgeld, d.h. der verbleibende Unterschied meines Eingangs, der zu einer anderen meiner Adressen zurückkehrt.

Am interessantesten ist natürlich die Verwendung von OP_RETURN in Ausgabe 0. Schauen wir uns genauer an, was es enthält:

![OP_RETURN-Ausgabe der Benachrichtigungstransaktion BIP47](assets/18.png)

Credit: https://blockstream.info/

Dort entdecken wir das Skript der Ausgabe in hexadezimaler Form:

> 6a4c50010002b13b2911719409d704ecc69f74fa315a6cb20fdd6ee39bc9874667703d67b164927b0e88f89f3f8b963549eab2533b5d7ed481a3bea7e953b546b4e91b6f50d800000000000000000000000000

In diesem Skript können wir mehrere Teile analysieren:
'>6a4c50010002b13b2911719409d704ecc69f74fa315a6cb20fdd6ee39bc9874667703d67b164927b0e88f89f3f8b963549eab2533b5d7ed481a3bea7e953b546b4e91b6f50d800000000000000000000000000>

> Des opcodes :

> 6a4c

> Un octet qui indique la taille de la charge utile (80 octets) :

> 50

> Les métadonnées de mon code de paiement en clair :

> 010002

> L'abscisse chiffrée de la clé publique de mon code de paiement :

> b13b2911719409d704ecc69f74fa315a6cb20fdd6ee39bc9874667703d67b164

> Le code de chaine chiffré de mon code de paiement :
> 927b0e88f89f3f8b963549eab2533b5d7ed481a3bea7e953b546b4e91b6f50d8

> Du rembourrage pour arriver à 80 octets :
> 00000000000000000000000000

Unter den Opcodes können wir 0x6a erkennen, der OP_RETURN bedeutet, und 0x4c, der OP_PUSHDATA1 bedeutet. Das nächste Byte nach diesem Opcode gibt die Größe der folgenden Nutzlast an. Es ist 0x50, also 80 Bytes.

Dann kommt der Zahlungscode mit der verschlüsselten Nutzlast.

Hier ist mein Zahlungscode in Klartext, der in dieser Transaktion verwendet wird:

> In Base 58:
>
> PM8TJQCyt6ovbozreUCBrfKqmSVmTzJ5vjqse58LnBzKFFZTwny3KfCDdwTqAEYVasn11tTMPc2FJsFygFd3YzsHvwNXLEQNADgxeGnMK8Ugmin62TZU
>
> In Base 16 (HEX):
> 4701000277507c9c17a89cfca2d3af554745d6c2db0e7f6b2721a3941a504933103cc42add94881210d6e752a9abc8a9fa0070e85184993c4f643f1121dd807dd556d1dc000000000000000000000000008604e4db

Wenn man meinen Zahlungscode im Klartext mit dem OP_RETURN vergleicht, kann man sehen, dass die HRP (in Braun) und die Prüfsumme (in Rosa) nicht übertragen werden. Das ist normal, diese Informationen sind für Menschen bestimmt.
Ensuite, on peut reconnaitre (en vert) la version (0x01), le champ de bits (0x00) et la parité de la clé publique (0x02). Et, à la fin du code de paiement, les octets vides en noir (0x00) qui permettent de rembourrer pour arriver à 80 octets au total. Toutes ces métadonnées sont transmises en clair (non chiffrées).

Enfin, on peut observer que l'abscisse de la clé publique (en bleu) et le code de chaîne (en rouge) ont été chiffrés. C'est ce qui constitue la charge utile du code de paiement.

### Réception de la transaction de notification.

Maintenant qu'Alice a envoyé la transaction de notification à Bob, voyons comment celui-ci l'interprète.

Pour rappel, Bob doit obligatoirement pouvoir accéder au code de paiement d'Alice. Sans cette information, comme nous allons le voir dans la partie suivante, il ne pourra pas dériver les paires de clés créées par Alice, et donc, il ne pourra pas accéder à ses bitcoins reçus avec BIP47. Pour le moment, la charge utile du code de paiement d'Alice est chiffrée. Voyons ensemble comment Bob la déchiffre.

1. Bob surveille les transactions qui créent des sorties avec son adresse de notification.

2. Lorsqu'une transaction dispose d'un output sur son adresse de notification, Bob l'analyse pour voir si elle contient une sortie OP_RETURN respectant le standard BIP47.

3. Si le premier octet de la charge utile de l'OP_RETURN est 0x01, Bob commence sa recherche d'un éventuel secret partagé avec ECDH :

- Bob sélectionne la clé publique en input de la transaction. C'est-à-dire la clé publique d'Alice nommée "A" avec :

> A = a·G

- Bob sélectionne la clé privée "b" associée à son adresse de notification personnelle :

> b

- Bob calcule le point secret "S" (secret partagé ECDH) sur la courbe elliptique par addition et doublement de points en appliquant sa clé privée "b" sur la clé publique d'Alice "A" :

> S = b·A

- Bob détermine le facteur aveuglant "f" qui va permettre de déchiffrer la charge utile du code de paiement d'Alice. De la même manière qu'Alice l'avait calculé précédemment, Bob va trouver "f" en appliquant HMAC-SHA512 sur (x) la valeur en abscisse du point secret "S", et sur (o) l'UTXO consommé en input de cette transaction de notification :

> f = HMAC-SHA512(o, x)

4. Bob interprète les données de l'OP_RETURN dans la transaction de notification comme un code de paiement. Il va simplement déchiffrer la charge utile de ce potentiel code de paiement grâce au facteur aveuglant "f" :

- Bob teilt den blinden Faktor "f" in zwei Teile auf: Die ersten 32 Bytes von "f" werden zu "f1" und die letzten 32 Bytes werden zu "f2".
- Bob entschlüsselt den verschlüsselten Abszissenwert (x') des öffentlichen Schlüssels des Zahlungscodes von Alice:

> x = x' XOR f1

- Bob entschlüsselt den verschlüsselten Kettencode (c') des Zahlungscodes von Alice:

> c = c' XOR f2

5. Bob überprüft, ob der öffentliche Schlüssel des Zahlungscodes von Alice zur Gruppe secp256k1 gehört. Wenn dies der Fall ist, interpretiert er dies als gültigen Zahlungscode. Andernfalls ignoriert er diese Transaktion.

Nun, da Bob den Zahlungscode von Alice kennt, kann sie ihm bis zu 2^32 Zahlungen senden, ohne jemals wieder eine Benachrichtigungstransaktion dieser Art durchführen zu müssen.

Warum funktioniert das? Wie kann Bob den gleichen blinden Faktor wie Alice bestimmen und somit ihren Zahlungscode entschlüsseln? Lassen Sie uns die Aktion von ECDH genauer betrachten, wie wir sie gerade beschrieben haben.

Zunächst haben wir es mit einer symmetrischen Verschlüsselung zu tun. Das bedeutet, dass der Verschlüsselungsschlüssel und der Entschlüsselungsschlüssel denselben Wert haben. Dieser Schlüssel in der Benachrichtigungstransaktion ist der blinde Faktor (f = f1 || f2). Alice und Bob müssen also denselben Wert für f erhalten, ohne ihn direkt zu übertragen, da ein Angreifer ihn stehlen und die geheime Information entschlüsseln könnte.

Dieser blinde Faktor wird erhalten, indem HMAC-SHA512 auf zwei Werte angewendet wird: die Abszisse eines geheimen Punktes und die in der Transaktion verwendete UTXO. Bob muss also über diese beiden Informationen verfügen, um die Nutzlast des Zahlungscodes von Alice zu entschlüsseln.

Für die Eingabe-UTXO kann Bob es einfach beobachten, indem er die Benachrichtigungstransaktion betrachtet. Für den geheimen Punkt muss Bob jedoch ECDH verwenden.

Wie in dem Abschnitt über Diffie-Hellman gesehen, können Alice und Bob einfach durch den Austausch ihrer jeweiligen öffentlichen Schlüssel und die geheime Anwendung ihrer privaten Schlüssel auf den öffentlichen Schlüssel des anderen einen bestimmten geheimen Punkt auf der elliptischen Kurve finden. Die Benachrichtigungstransaktion stützt sich auf diesen Mechanismus:

> Bobs Schlüsselpaar:
>
> B = b·G
>
> Alice' Schlüsselpaar:
>
> A = a·G
>
> Für einen geheimen Punkt S (x, y):
>
> S = a·B = a·b·G = b·a·G = b·A

![Generierung eines gemeinsamen Geheimnisses mit ECDHE-Diagramm](assets/19.png)
Jetzt, da Bob den Zahlungscode von Alice kennt, wird er in der Lage sein, ihre BIP47-Zahlungen zu erkennen und die empfangenen Bitcoins zu entschlüsseln, indem er die entsprechenden privaten Schlüssel ableitet.
![Bob interpretiert die Benachrichtigungstransaktion von Alice](assets/20.png)

Quelle: Wiederverwendbare Zahlungscodes für hierarchisch deterministische Wallets, Justus Ranvier. https://github.com/bitcoin/bips/blob/master/bip-0047.mediawiki

Wenn wir dieses Schema mit dem vergleichen, was ich Ihnen zuvor beschrieben habe:

- "Wallet Pub-Key" auf Alice's Seite entspricht: A.

- "Child Priv-Key 0" auf Bob's Seite entspricht: b.

- "Notification Shared Secret" entspricht: f.

- "Masked Payment Code" entspricht dem verschleierten Zahlungscode von Alice, d.h. mit verschlüsseltem Payload: x' und c'.

- "Notification Transaction" ist die Transaktion, die den OP_RETURN enthält.

Ich fasse die Schritte zusammen, die wir gerade gemeinsam gesehen haben, um eine Benachrichtigungstransaktion zu empfangen und zu interpretieren:

- Bob überwacht die Transaktionsausgänge an seine Benachrichtigungsadresse.

- Wenn er eine entdeckt, ruft er die Informationen aus dem OP_RETURN ab.

- Bob wählt den öffentlichen Schlüssel als Eingabe aus und berechnet einen geheimen Punkt mit ECDH.

- Er verwendet diesen geheimen Punkt, um einen HMAC zu berechnen, der als Verblindungsfaktor dient.

- Er verwendet diesen Verblindungsfaktor, um den Payload des Zahlungscodes von Alice im OP_RETURN zu entschlüsseln.

### Die BIP47-Zahlungstransaktion.

Lassen Sie uns nun gemeinsam den Zahlungsprozess mit BIP47 betrachten. Um den aktuellen Stand der Situation in Erinnerung zu rufen:

- Alice kennt den Zahlungscode von Bob, den sie einfach von seiner Website erhalten hat.

- Bob kennt den Zahlungscode von Alice dank der Benachrichtigungstransaktion.

- Alice wird eine erste Zahlung an Bob durchführen. Sie kann weitere Zahlungen auf die gleiche Weise durchführen.

Bevor ich Ihnen diesen Prozess erkläre, denke ich, es ist wichtig, sich daran zu erinnern, an welchen Indizes wir derzeit arbeiten:

Der Ableitungspfad eines Zahlungscodes wird wie folgt beschrieben: m/47'/0'/0'/.

Der nächste Tiefenbereich verteilt die Indizes wie folgt:

- Das erste normale Kindpaar (nicht verstärkt) wird verwendet, um die Benachrichtigungsadresse zu generieren, über die wir im vorherigen Teil gesprochen haben: m/47'/0'/0'/0/.

- Normale Kindschlüsselpaare werden innerhalb von ECDH verwendet, um BIP47-Zahlungsempfangsadressen zu generieren, wie wir in diesem Teil sehen werden: m/47'/0'/0'/ von 0 bis 2 147 483 647/.

- Verstärkte Kindschlüsselpaare sind ephemere Zahlungscodes: m/47'/0'/0'/ von 0' bis 2 147 483 647'/.'
  Jedes Mal, wenn Alice eine Zahlung an Bob senden möchte, leitet sie eine neue eindeutige leere Adresse ab, wieder dank des ECDH-Protokolls:
- Alice wählt den ersten abgeleiteten privaten Schlüssel aus ihrem wiederverwendbaren persönlichen Zahlungscode aus:

> a

- Alice wählt den ersten unbenutzten öffentlichen Schlüssel aus, der aus Bobs Zahlungscode abgeleitet wurde. Diesen öffentlichen Schlüssel nennen wir "B". Er ist mit dem privaten Schlüssel "b" verbunden, von dem nur Bob Kenntnis hat.

> B = b·G

- Alice berechnet einen geheimen Punkt "S" auf der elliptischen Kurve, indem sie ihren privaten Schlüssel "a" auf Bobs öffentlichen Schlüssel "B" anwendet, indem sie Punkte addiert und verdoppelt:

> S = a·B

- Aus diesem geheimen Punkt berechnet Alice das gemeinsame Geheimnis "s" (kleingeschrieben). Dazu wählt sie die Abszisse des geheimen Punktes "S", die als "Sx" bezeichnet wird, und gibt diesen Wert in die SHA256-Hashfunktion ein.

> s = SHA256(Sx)

Vertraue nicht. Überprüfe! Wenn Sie die Grundprinzipien einer Hashfunktion verstehen möchten, finden Sie in diesem Artikel weitere Informationen. Und wenn Sie dem NIST nicht vertrauen (zu Recht) und den genauen Ablauf von SHA256 verstehen möchten, erkläre ich Ihnen alles in diesem Artikel auf Französisch.

- Alice verwendet dieses gemeinsame Geheimnis "s", um eine Bitcoin-Empfangsadresse zu berechnen. Zunächst überprüft sie, ob "s" im Bereich der Kurve secp256k1 enthalten ist. Wenn dies nicht der Fall ist, erhöht sie den Index des öffentlichen Schlüssels von Bob, um ein anderes gemeinsames Geheimnis abzuleiten.

- Anschließend berechnet sie einen öffentlichen Schlüssel "K0", indem sie auf der elliptischen Kurve die Punkte "B" und "s·G" addiert. Mit anderen Worten, Alice addiert den aus Bobs Zahlungscode abgeleiteten öffentlichen Schlüssel "B" mit einem anderen Punkt, der auf der elliptischen Kurve durch Addition und Verdopplung von Punkten mit dem gemeinsamen Geheimnis "s" vom Generatorpunkt der Kurve secp256k1 "G" berechnet wird. Dieser neue Punkt repräsentiert einen öffentlichen Schlüssel, den wir "K0" nennen:

> K0 = B + s·G

- Mit diesem öffentlichen Schlüssel "K0" kann Alice eine leere Empfangsadresse auf standardmäßige Weise ableiten (z. B. SegWit V0 in Bech32).

Sobald Alice diese Empfangsadresse "K0" von Bob hat, kann sie eine herkömmliche Bitcoin-Transaktion erstellen, indem sie eine UTXO auswählt, die ihr in einem anderen Zweig ihrer HD-Brieftasche gehört, und sie an die Adresse "K0" von Bob ausgibt.

![Alice sendet Bitcoins mit BIP47 an Bob](assets/21.png)

Credit: Wiederverwendbare Zahlungscodes für hierarchisch deterministische Geldbörsen, Justus Ranvier. https://github.com/bitcoin/bips/blob/master/bip-0047.mediawiki
Wenn wir dieses Schema mit dem vergleichen, was ich Ihnen zuvor beschrieben habe:

- "Child Priv-Key" auf der Seite von Alice entspricht: a.

- "Child Pub-Key 0" auf der Seite von Bob entspricht: B.

- "Payment Secret 0" entspricht: s.

- "Payment Pub-Key 0" entspricht: K0.

Ich fasse die Schritte zusammen, die wir gerade gemeinsam für eine BIP47-Zahlung durchgegangen sind:

- Alice wählt den ersten abgeleiteten privaten Schlüssel aus ihrem persönlichen Zahlungscode aus.

- Sie berechnet einen geheimen Punkt auf der elliptischen Kurve mit ECDH aus dem ersten unbenutzten abgeleiteten öffentlichen Schlüssel aus Bobs Zahlungscode.

- Sie verwendet diesen geheimen Punkt, um ein gemeinsames Geheimnis mit SHA256 zu berechnen.

- Sie verwendet dieses gemeinsame Geheimnis, um einen neuen geheimen Punkt auf der elliptischen Kurve zu berechnen.

- Sie addiert diesen neuen geheimen Punkt zum öffentlichen Schlüssel von Bob.

- Sie erhält einen neuen ephemeren öffentlichen Schlüssel, für den nur Bob den zugehörigen privaten Schlüssel besitzt.

- Alice kann eine normale Transaktion an Bob mit der abgeleiteten ephemeren Empfangsadresse senden.

Wenn sie eine zweite Zahlung durchführen möchte, wiederholt sie die oben genannten Schritte, außer dass sie den zweiten abgeleiteten öffentlichen Schlüssel aus Bobs Zahlungscode auswählt. Das bedeutet, den nächsten unbenutzten Schlüssel. Sie hat dann eine zweite Empfangsadresse, die zu Bob gehört, "K1".

![Alice leitet drei BIP47-Empfangsadressen an Bob ab](assets/22.png)

Credit: Wiederverwendbare Zahlungscodes für hierarchisch deterministische Wallets, Justus Ranvier. https://github.com/bitcoin/bips/blob/master/bip-0047.mediawiki

Sie kann auf diese Weise fortsetzen und bis zu 2^32 leere Adressen ableiten, die zu Bob gehören.

Aus externer Sicht, bei Beobachtung der Bitcoin-Blockchain, ist es theoretisch unmöglich, eine BIP47-Zahlung von einer normalen Zahlung zu unterscheiden. Hier ist ein Beispiel für eine BIP47-Zahlungstransaktion im Testnetz:

https://blockstream.info/testnet/tx/94b2e59510f2e1fa78411634c98a77bbb638e28fb2da00c9f359cd5fc8f87254

TXID:

> 94b2e59510f2e1fa78411634c98a77bbb638e28fb2da00c9f359cd5fc8f87254

Es sieht aus wie eine normale Transaktion mit einer verbrauchten Eingabe, einer Zahlungsausgabe von 210.000 Sats und einer Wechselgeldausgabe:

![Bitcoin-Zahlungstransaktion mit BIP47](assets/23.png)

Credit: https://blockstream.info/

### Empfang einer BIP47-Zahlung und Ableitung des privaten Schlüssels.

Alice hat gerade ihre erste Zahlung an eine leere BIP47-Adresse gesendet, die Bob gehört. Lassen Sie uns nun gemeinsam sehen, wie Bob diese Zahlung empfängt. Wir werden auch sehen, warum Alice keinen Zugriff auf den privaten Schlüssel der Adresse hat, den sie gerade generiert hat, und wie Bob diesen Schlüssel findet, um die Bitcoins auszugeben, die er gerade erhalten hat.
Sobald Bob die Benachrichtigungstransaktion von Alice erhält, leitet er den BIP47-Public Key "K0" ab, noch bevor sie eine Zahlung dorthin gesendet hat. Er beobachtet also jede Zahlung an die zugehörige Adresse. Tatsächlich leitet er sofort mehrere Adressen ab, die er beobachten wird (K0, K1, K2, K3...). So leitet er den BIP47-Public Key "K0" ab:

- Bob wählt den ersten abgeleiteten privaten Schlüssel aus seinem Zahlungscode aus. Dieser private Schlüssel wird "b" genannt und ist mit dem öffentlichen Schlüssel "B" verbunden, mit dem Alice in dem vorherigen Schritt ihre Berechnungen durchgeführt hat:

> b

- Bob wählt den ersten abgeleiteten öffentlichen Schlüssel von Alice aus ihrem Zahlungscode aus. Dieser Schlüssel wird "A" genannt und ist mit dem privaten Schlüssel "a" verbunden, den nur Alice kennt. Bob kann diesen Prozess durchführen, da er den Zahlungscode von Alice kennt, der ihm zusammen mit der Benachrichtigungstransaktion übermittelt wurde.

> A = a·G

- Bob berechnet den geheimen Punkt "S", indem er seine private Schlüssel "b" auf den öffentlichen Schlüssel von Alice "A" anwendet und Punkte auf der elliptischen Kurve addiert und verdoppelt. Hier verwenden wir ECDH, das sicherstellt, dass dieser Punkt "S" für Bob und Alice gleich ist.

> S = b·A

- Auf die gleiche Weise wie Alice isoliert Bob die x-Koordinate dieses Punktes "S". Wir haben diesen Wert "Sx" genannt. Er gibt diesen Wert in die SHA256-Funktion ein, um das gemeinsame Geheimnis "s" zu finden (kleingeschrieben).

> s = SHA256(Sx)

- Wie Alice berechnet Bob den Punkt "s·G" auf der elliptischen Kurve. Dann addiert er diesen geheimen Punkt mit seinem öffentlichen Schlüssel "B". Er erhält einen neuen Punkt auf der elliptischen Kurve, den er als öffentlichen Schlüssel "K0" interpretiert:

> K0 = B + s·G

Sobald Bob diesen öffentlichen Schlüssel "K0" hat, kann er den zugehörigen privaten Schlüssel ableiten, um seine Bitcoins ausgeben zu können. Nur er kann diese Zahl generieren.

- Bob addiert seinen abgeleiteten privaten Schlüssel "b" aus seinem persönlichen Zahlungscode. Nur er kann den Wert von "b" erhalten. Dann addiert er "b" mit dem gemeinsamen Geheimnis "s", um k0, den privaten Schlüssel von K0, zu erhalten:

> k0 = b + s
> Dank des Gruppenrechts der elliptischen Kurve erhält Bob genau den privaten Schlüssel, der dem von Alice verwendeten öffentlichen Schlüssel entspricht. Wir haben also:
> K0 = k0·G

![Bob generiert seine BIP47-Empfangsadressen](assets/24.png)

Credit: Wiederverwendbare Zahlungscodes für hierarchisch deterministische Wallets, Justus Ranvier. https://github.com/bitcoin/bips/blob/master/bip-0047.mediawiki

Wenn wir dieses Schema mit dem vergleichen, was ich Ihnen zuvor beschrieben habe:

- "Child Priv-Key 0" auf Bobs Seite entspricht: b.

- "Child Pub-Key 0" auf Alice' Seite entspricht: A.

- "Payment Secret 0" entspricht: s.

- "Payment Pub-Key 0" entspricht: K0.

- "Payment Priv-Key 0" entspricht: k0.

Ich fasse die Schritte zusammen, die wir gerade gemeinsam durchgegangen sind, um eine BIP47-Zahlung zu empfangen und den entsprechenden privaten Schlüssel zu berechnen:

- Bob wählt den ersten abgeleiteten Kind-Privatschlüssel aus seinem persönlichen Zahlungscode aus.

- Er berechnet einen geheimen Punkt auf der elliptischen Kurve durch ECDH aus dem ersten abgeleiteten Kind-Publikumsschlüssel aus Alices Kettencode.

- Er verwendet diesen geheimen Punkt, um ein mit SHA256 gemeinsam genutztes Geheimnis zu berechnen.

- Er verwendet dieses gemeinsam genutzte Geheimnis, um einen neuen geheimen Punkt auf der elliptischen Kurve zu berechnen.

- Er addiert diesen neuen geheimen Punkt zu seinem persönlichen öffentlichen Schlüssel.

- Er erhält einen neuen ephemeren öffentlichen Schlüssel, an den Alice ihre erste Zahlung senden wird.

- Bob berechnet den mit diesem ephemeren öffentlichen Schlüssel verbundenen privaten Schlüssel, indem er seinen abgeleiteten Kind-Privatschlüssel aus seinem Zahlungscode und das gemeinsam genutzte Geheimnis addiert.

Da Alice nicht "b", Bobs privaten Schlüssel, erhalten kann, ist sie nicht in der Lage, k0, den privaten Schlüssel, der der BIP47-Empfangsadresse von Bob zugeordnet ist, zu bestimmen.

Schematisch können wir die Berechnung des gemeinsam genutzten Geheimnisses "S" wie folgt darstellen:

![Berechnung des gemeinsam genutzten Geheimnisses mit ECDHE](assets/25.png)

Nachdem das gemeinsam genutzte Geheimnis mit ECDH gefunden wurde, berechnen Alice und Bob den BIP47-Zahlungspublikumsschlüssel "K0", und Bob berechnet auch den zugehörigen privaten Schlüssel "k0":

![Ableitung der BIP47-Empfangsadresse aus dem gemeinsam genutzten Geheimnis](assets/26.png)

### Rückerstattung der BIP47-Zahlung.

Da Bob den wiederverwendbaren Zahlungscode von Alice kennt, hat er bereits alle erforderlichen Informationen, um ihr eine Rückerstattung zu senden. Er muss Alice nicht erneut kontaktieren, um nach irgendwelchen Informationen zu fragen. Er muss sie lediglich mit einer Benachrichtigungstransaktion informieren, insbesondere damit sie ihre BIP47-Adressen mit ihrem Seed wiederherstellen kann, und dann kann er ihr bis zu 2^32 Zahlungen senden.
Bob kann Alice dann auf die gleiche Weise zurückerstatten, wie sie ihm Zahlungen geschickt hat. Die Rollen kehren sich um:

![Bob sendet Alice eine Rückerstattung mit BIP47](assets/27.png)

Credit: Wiederverwendbare Zahlungscodes für hierarchisch deterministische Wallets, Justus Ranvier. https://github.com/bitcoin/bips/blob/master/bip-0047.mediawiki

Jetzt kennen Sie alle Feinheiten dieser großartigen Lösung namens BIP47.

## Abgeleitete Verwendungen von PayNym.

Die Implementierung von BIP47 in der Samourai Wallet hat zu den PayNym geführt, Identifikatoren, die aus den Zahlungscodes der Benutzer berechnet werden. Heute geht ihr Nutzen weit über die Verwendung von BIP47 hinaus.

Das Samourai-Team entwickelt allmählich ein ganzes Ökosystem von Tools und Diensten rund um den Benutzer-PayNym. Dazu gehören natürlich alle Ausgabewerkzeuge, die die Benutzerprivatsphäre optimieren, indem sie einer Transaktion Entropie hinzufügen und somit plausible Abstreitbarkeit gewährleisten.

Die gemeinsame Nutzung von Soroban, dem auf Tor basierenden verschlüsselten Kommunikationsnetzwerk, und PayNym hat die Benutzererfahrung bei der Erstellung von gemeinsamen Transaktionen erheblich verbessert und gleichzeitig ein hohes Maß an Sicherheit gewährleistet. So können Stowaway (PayJoin) und StonewallX2-Transaktionen leicht durchgeführt werden, ohne die vielen Austausche von nicht signierten Transaktionen manuell durchführen zu müssen, die für die Durchführung einer solchen gemeinsamen Transaktion erforderlich sind.

Im Gegensatz zur Verwendung von BIP47 müssen bei diesen gemeinsamen Transaktionen keine Benachrichtigungstransaktionen durchgeführt werden. Es reicht aus, die PayNym zu verknüpfen, um diese Tools zu verwenden. Es ist keine Verbindung erforderlich.

Wenn Sie mehr über gemeinsame Transaktionen und im Allgemeinen über alle Ausgabewerkzeuge der Samourai Wallet erfahren möchten, können Sie den Abschnitt "Ausgabewerkzeuge" in diesem Artikel lesen. Dort finden Sie eine technische Erklärung und eine detaillierte Anleitung für jedes Tool.

Neben diesen gemeinsamen Transaktionen wurde kürzlich beobachtet, dass das Samourai-Team an einem mit PayNym verbundenen Authentifizierungsprotokoll arbeitet: Auth47. Dieses Tool ist bereits implementiert und ermöglicht beispielsweise die Authentifizierung mit einem PayNym auf einer Website, die diese Methode akzeptiert. In Zukunft denke ich, dass Auth47 über diese Möglichkeit der Web-Authentifizierung hinaus in ein umfassenderes Projekt rund um das BIP47/PayNym/Samourai-Ökosystem integriert wird. Möglicherweise wird dieses Protokoll verwendet, um die Benutzererfahrung der Samourai Wallet weiter zu optimieren, insbesondere bei der Verwendung von Ausgabewerkzeugen. Es bleibt abzuwarten...

## Meine persönliche Meinung zu BIP47.

'Natürlich ist der Hauptnachteil von BIP47 die Transaktionsbenachrichtigung. Der Benutzer muss Gebühren für das Mining dieser Transaktion bezahlen, was für einige lästig sein kann. Die Argumentation bezüglich des "Spams" in der Bitcoin-Blockchain ist jedoch absolut unannehmbar. Jeder, der die Gebühren für seine Transaktion bezahlt, sollte in der Lage sein, diese in das Register einzutragen, unabhängig von ihrem Zweck. Das Gegenteil zu behaupten bedeutet, sich für Zensur auszusprechen.

Es ist möglich, dass in Zukunft kostengünstigere Lösungen gefunden werden, um den Zahlungscode des Absenders an den Empfänger zu übermitteln und dieser ihn sicher zu speichern. Aber im Moment ist die Transaktionsbenachrichtigung die Lösung mit den wenigsten Kompromissen.

Dieser Nachteil ist vernachlässigbar, wenn man alle Vorteile von BIP47 betrachtet. Unter allen bestehenden Vorschlägen zur Lösung dieses Problems der Adresswiederverwendung scheint es mir die beste Lösung zu sein.

Wie bereits erklärt, stammen die meisten Adresswiederverwendungen von Börsen. BIP47 ist die einzige vernünftige Lösung, die dieses Problem tatsächlich an der Quelle löst. Jeder Vorschlag, die Anzahl der Adresswiederverwendungen zu reduzieren, sollte diesen Aspekt berücksichtigen und die Lösung an die Hauptquelle des Problems anpassen.

In Bezug auf die Verwendung ist das BIP47-Zahlungsverfahren trotz seiner komplexen Mechanismen kinderleicht. Wiederverwendbare Zahlungscodes können daher auch von unerfahrenen Benutzern problemlos übernommen werden.

In Bezug auf die Privatsphäre ist BIP47 sehr interessant. Wie bereits im Abschnitt zur Transaktionsbenachrichtigung erklärt, enthüllt der Zahlungscode keine Informationen über abgeleitete temporäre Adressen. Dadurch wird der Informationsfluss zwischen der Bitcoin-Transaktion und der Empfänger-ID unterbrochen, im Gegensatz zur herkömmlichen Verwendung einer Empfangsadresse.

Und vor allem funktioniert die PayNym-Implementierung von BIP47! Sie ist seit 2016 in der Samourai Wallet verfügbar und seit Anfang dieses Jahres in der Sparrow Wallet. Es handelt sich nicht um ein wissenschaftliches Projekt, sondern um eine gestern getestete und heute voll funktionsfähige Lösung.

Hoffentlich werden diese wiederverwendbaren Zahlungscodes in Zukunft von den Akteuren im Ökosystem übernommen, in Wallet-Software implementiert und von Bitcoin-Nutzern verwendet.

Jede wirklich positive Lösung für die Benutzerprivatsphäre muss diskutiert, vorangetrieben und verteidigt werden, damit Bitcoin nicht zum Spielplatz von CA wird und zum Überwachungsinstrument der Regierungen wird.'
'> Er dachte daran, wie er überall verfolgt und beleidigt worden war, und jetzt hörte er alle sagen, dass er der schönste aller schönen Vögel sei! Selbst der Holunder neigte seine Zweige zu ihm hin und die Sonne verbreitete ein so warmes und wohltuendes Licht! Da blähten sich seine Federn auf, sein schlanker Hals richtete sich auf und er rief aus vollem Herzen: "Wie konnte ich so viel Glück träumen, als ich nur eine hässliche kleine Ente war."

## Weitere Informationen:

- Verstehen und Verwenden von CoinJoin auf Bitcoin.

- Verstehen der Derivationspfade einer Bitcoin-Wallet.

- Installation und Verwendung des Bitcoin-Knotens RoninDojo.

### Externe Ressourcen und Dank:

    Vielen Dank an LaurentMT und Théo Pantamis für die vielen Konzepte, die sie mir erklärt haben und die ich in diesem Artikel verwendet habe. Ich hoffe, ich habe sie genau wiedergegeben.

    Vielen Dank an Fanis Michalakis für das Korrekturlesen dieses Textes und seine fachlichen Ratschläge.

    https://bitcoiner.guide/paynym/

    https://github.com/bitcoin/bips/blob/master/bip-0047.mediawiki

    https://fr.wikipedia.org/wiki/%C3%89change_de_cl%C3%A9s_Diffie-Hellman

    https://fr.wikipedia.org/wiki/%C3%89change_de_cl%C3%A9s_Diffie-Hellman_bas%C3%A9_sur_les_courbes_elliptiques

    https://security.stackexchange.com/questions/46802/what-is-the-difference-between-dhe-and-ecdh#:~:text=The%20difference%20between%20DHE%20and%20ECDH%20in%20two%20bullet%20points,a%20type%20of%20algebraic%20curve).

    https://commandlinefanatic.com/cgi-bin/showarticle.cgi?article=art060

    https://ee.stanford.edu/~hellman/publications/24.pdf

    https://www.researchgate.net/publication/317339928_A_study_on_diffie-hellman_key_exchange_protocols'
