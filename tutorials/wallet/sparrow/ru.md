---
name: Воробей Wallet
description: Установка, настройка и использование Sparrow Wallet
---
![cover](assets/cover.webp)

Sparrow Wallet - это программное обеспечение для управления портфелем Bitcoin, разработанное Крейгом Роу. Это программное обеспечение с открытым исходным кодом ценится биткоинщиками за множество функций и интуитивно понятный Interface.

Использовать Sparrow можно двумя способами:


- Например, Hot Wallet, где ваши закрытые ключи хранятся на вашем компьютере.
- В качестве менеджера Cold Wallet, где приватные ключи хранятся на Hardware Wallet. В этом режиме Sparrow манипулирует только публичной информацией Wallet, отслеживает средства, генерирует адреса и создает транзакции, но для того, чтобы эти транзакции были действительными, требуется подпись Hardware Wallet. Поэтому он может заменить такие приложения, как Ledger Live или Trezor Suite.

Sparrow поддерживает кошельки с одной и несколькими подписями и позволяет плавно управлять несколькими кошельками. Например, вы можете одновременно управлять одним Wallet, подключенным к Ledger, другим - к Trezor, а также иметь Hot Wallet.

Программное обеспечение также предлагает расширенные функции контроля монет, позволяя вам точно выбирать, какие UTXO использовать в ваших сделках, чтобы оптимизировать вашу конфиденциальность.

Что касается подключения, Sparrow позволяет вам подключаться к собственному узлу Bitcoin, либо удаленно через Electrum Server, либо с помощью Bitcoin Core. Также можно использовать публичную ноду, если у вас еще нет своей. Удаленные соединения осуществляются через Tor.

## Установить воробья Wallet

Перейдите на [официальную страницу загрузки Sparrow Wallet] (https://sparrowwallet.com/download/) и выберите версию программного обеспечения, соответствующую вашей операционной системе.

![Image](assets/fr/01.webp)

Важно проверить целостность и подлинность программного обеспечения перед его установкой. Если вы не знаете, как это сделать, полное руководство вы найдете здесь:

https://planb.network/tutorials/computer-security/data/integrity-authenticity-21d0420a-be02-4663-94a3-8d487f23becc
После установки Sparrow вы можете пропустить первые поясняющие экраны и сразу перейти к экрану управления соединениями.

![Image](assets/fr/02.webp)

## Подключение к сети Bitcoin

Чтобы взаимодействовать с сетью Bitcoin и транслировать свои транзакции, Sparrow должен быть подключен к узлу Bitcoin. Существует три основных способа установить такое соединение:


- 🟡 Использование публичного узла, т. е. подключение к стороннему узлу, который разрешает такие подключения. Если у вас нет собственного узла Bitcoin, этот вариант позволит вам быстро начать работу с Sparrow. Однако узел, к которому вы подключитесь, будет видеть все ваши транзакции, что может нарушить вашу конфиденциальность. Контроль над своими ключами очень важен, но наличие собственного узла еще лучше. Поэтому используйте эту опцию только в том случае, если вы только начинаете, осознавая при этом риски для вашей конфиденциальности.
- 🟢 Подключение к узлу Bitcoin Core. Если у вас есть собственный узел Bitcoin Core, вы можете подключить его к Sparrow Wallet либо локально, если Bitcoin Core установлен на той же машине, либо удаленно.
- 🔵 Подключение через сервер Electrum. Если ваш узел Bitcoin оснащен сервером Electrs, как в случае с решениями "узел-в-коробке", такими как Umbrel или Start9, вы можете удаленно подключиться к нему из Sparrow.

**Предпочтительно использовать соединение через Electrs или Bitcoin Core на собственном узле, чтобы уменьшить необходимость доверять третьей стороне и оптимизировать конфиденциальность**

### Подключение к публичному узлу 🟡

Подключиться к публичному узлу очень просто. Перейдите на вкладку "*Общественный сервер*".

![Image](assets/fr/03.webp)

Выберите узел из раскрывающегося списка.

![Image](assets/fr/04.webp)

Затем нажмите на кнопку "*Тестовое соединение*".

![Image](assets/fr/05.webp)

После подключения Sparrow Wallet отобразит желтую галочку в правом нижнем углу Interface, чтобы указать, что вы подключены к публичному узлу.

![Image](assets/fr/06.webp)

### Подключение к ядру Bitcoin 🟢

Второй способ подключения к узлу Bitcoin - связать Sparrow с Bitcoin Core. Если Bitcoin Core установлен на той же машине, аутентификация будет осуществляться через файл cookie. Если Bitcoin Core находится на удаленной машине, вам нужно будет использовать пароль, заданный в файле `Bitcoin.conf`.

Обратите внимание, что если вы используете обрезанный узел Bitcoin Core, вы не сможете восстановить Wallet, содержащий транзакции, предшествующие локально сохраненным блокам. Однако для нового Wallet, созданного на Sparrow, это не будет проблемой: ваши новые транзакции будут видны даже при обрезанном узле.

Чтобы настроить узел Bitcoin Core, вы можете обратиться к одному из следующих руководств, в зависимости от вашей операционной системы:

https://planb.network/tutorials/node/bitcoin/bitcoin-core-mac-windows-9684ab02-e0af-41c9-8102-86ac7c7727f3
https://planb.network/tutorials/node/bitcoin/bitcoin-core-linux-568c13a6-8746-4d63-8e95-f4a61c5ae0ed
На сайте Sparrow перейдите на вкладку "*Bitcoin Core*".

![Image](assets/fr/07.webp)

**С Bitcoin Core local:**

Если на вашем компьютере установлен Bitcoin Core, найдите файл `Bitcoin.conf` среди файлов программного обеспечения. Если этот файл не существует, вы можете создать его. Откройте его с помощью текстового редактора и вставьте следующую строку:

```ini
server=1
````
Sauvegardez ensuite vos modifications.
Vous pouvez également effectuer cette configuration via l'interface graphique de Bitcoin-QT en naviguant dans "*Settings*" > "*Options...*" et en activant l'option "*Enable RPC server*".
N'oubliez pas de redémarrer le logiciel après ces modifications.
![Image](assets/fr/08.webp)
Revenez ensuite à Sparrow Wallet et renseignez le chemin vers votre fichier de cookie, généralement situé dans le même dossier que le `bitcoin.conf`, selon votre système d'exploitation :
| **macOS**   | ~/Library/Application Support/Bitcoin |
| ----------- | ------------------------------------- |
| **Windows** | %APPDATA%\Bitcoin                     |
| **Linux**   | ~/.bitcoin                            |
![Image](assets/fr/09.webp)
Laissez les autres paramètres par défaut, l'URL `127.0.0.1` et le port `8332`, puis cliquez sur "*Test Connection*".
![Image](assets/fr/10.webp)
La connexion est établie. Une coche verte apparaîtra en bas à droite pour indiquer que vous êtes connecté à un nœud Bitcoin Core.
![Image](assets/fr/11.webp)
**Avec Bitcoin Core à distance :**
Si Bitcoin Core est installé sur une autre machine connectée sur le même réseau, commencez par localiser le fichier `bitcoin.conf` parmi les fichiers du logiciel. Si ce fichier n'existe pas encore, vous pouvez le créer. Ouvrez ce fichier avec un éditeur de texte et ajoutez la ligne suivante :
```

сервер=1

```
Après avoir modifié le fichier, assurez-vous de l'enregistrer dans le dossier approprié selon votre système d'exploitation :
| **macOS**   | ~/Library/Application Support/Bitcoin |
| ----------- | ------------------------------------- |
| **Windows** | %APPDATA%\Bitcoin                     |
| **Linux**   | ~/.bitcoin                            |
Il est également possible de réaliser cette manipulation via l'interface graphique de Bitcoin-QT. Accédez au menu "*Settings*", puis "*Options...*", et activez l'option "*Enable RPC server*" en cochant la case correspondante. Si le fichier `bitcoin.conf` n'existe pas, vous pouvez le créer directement depuis cette interface en cliquant sur "*Open Configuration File*".
![Image](assets/fr/12.webp)
Trouvez l'adresse IP de la machine qui héberge Bitcoin Core dans votre réseau local. Pour cela, vous pouvez utiliser un outil tel que [Angry IP Scanner](https://angryip.org/). Supposons, pour l'exemple, que l'adresse IP de votre nœud soit `192.168.1.18`.
Dans le fichier `bitcoin.conf`, ajoutez les lignes suivantes, en configurant `rpcbind=192.168.1.18` pour correspondre à l'adresse IP de votre nœud.
```

[рука]

rpcbind=127.0.0.1

rpcbind=192.168.1.18

rpcallowip=127.0.0.1

rpcallowip=192.168.1.0/24

```
![Image](assets/fr/13.webp)
Ajoutez également dans le fichier `bitcoin.conf` un identifiant et un mot de passe pour les connexions à distance. Assurez-vous de remplacer `loic` par votre nom d'utilisateur et `my_password` par un mot de passe fort :
```

rpcuser=loic

rpcpassword=my_password

```