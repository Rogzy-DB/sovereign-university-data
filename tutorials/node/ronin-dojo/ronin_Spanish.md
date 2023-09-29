---
name: RoninDojo

description: Instalar y utilizar su propio nodo Bitcoin RoninDojo.
---

# Instalar y utilizar su propio nodo Bitcoin RoninDojo.

Ejecutar y utilizar su propio nodo es esencial para participar realmente en la red de Bitcoin. Aunque ejecutar un nodo Bitcoin no proporciona ninguna ventaja económica al usuario, le permite preservar su privacidad, actuar de manera independiente y tener control sobre su confianza en la red.

En este artículo, examinaremos en detalle RoninDojo, una excelente solución para ejecutar su propio nodo Bitcoin.

### Resumen:

- ¿Qué es RoninDojo?
- ¿Qué hardware elegir?
- ¿Cómo instalar RoninDojo?
- ¿Cómo utilizar RoninDojo?
- Conclusión

Si no está familiarizado con el funcionamiento y el papel de un nodo Bitcoin, le recomiendo que comience leyendo este artículo: El nodo Bitcoin - Parte 1/2: Conceptos técnicos.

![Samourai](assets/1.png)

## ¿Qué es RoninDojo?

Dojo es un servidor de nodo completo de Bitcoin desarrollado por el equipo de Samouraï Wallet. Puede instalarlo libremente en cualquier máquina.

RoninDojo es una herramienta de instalación y administración para Dojo y varias otras herramientas. RoninDojo toma la implementación original de Dojo y agrega muchas otras herramientas, facilitando su instalación y gestión.

También ofrecen un hardware "plug-and-play", el RoninDojo Tanto, con RoninDojo preinstalado en una máquina ensamblada por su equipo. El Tanto es una solución de pago interesante para aquellos que no quieren ensuciarse las manos.

El código de RoninDojo es de código abierto, por lo que también es posible instalar esta solución en su propio hardware. Esta opción es económica, pero requiere un poco más de manipulación, que es lo que haremos en este artículo.

RoninDojo es un Dojo, por lo que permite integrar fácilmente Whirlpool CLI en su nodo Bitcoin para tener la mejor experiencia posible de CoinJoin. Con Whirlpool CLI, no solo puede mezclar sus bitcoins las 24 horas del día, los 7 días de la semana sin tener que dejar encendida su computadora personal, sino que también puede mejorar significativamente su privacidad.

RoninDojo incluye muchas otras herramientas que se basan en su Dojo, como el calculador Boltzmann que permite determinar el grado de privacidad de una transacción, el servidor Electrum para conectar sus diferentes billeteras Bitcoin a su nodo, o el servidor Mempool para observar sus transacciones de forma privada.
En comparación con otra solución de nodo como Umbrel, que les presenté en este artículo, RoninDojo se enmarca en una línea de desarrollo profundamente orientada hacia soluciones "On Chain" y herramientas que optimizan la privacidad de los usuarios. Por lo tanto, RoninDojo no permite interactuar con la Lightning Network.
RoninDojo ofrece menos herramientas en comparación con Umbrel, pero las pocas características esenciales para un Bitcoiner presentes en Ronin son increíblemente estables.

Entonces, si no necesitas todas las características de un servidor Umbrel y solo quieres tener un nodo simple y estable con algunas herramientas esenciales como Whirlpool o Mempool, entonces RoninDojo seguramente es una buena solución para ti.

En mi opinión, la línea de desarrollo de Umbrel está muy orientada hacia la Lightning Network y herramientas versátiles. Aunque sigue siendo un nodo Bitcoin, se busca convertirlo en un mini-servidor multitarea. Por otro lado, la línea de desarrollo de RoninDojo se acerca más a la de los equipos de Samourai Wallet y se enfoca en las herramientas esenciales de un Bitcoiner que le permiten tener plena independencia y una gestión optimizada de su privacidad en Bitcoin.

Ten en cuenta que configurar un nodo RoninDojo es ligeramente más complejo que configurar un nodo Umbrel.

Ahora que hemos podido describir a RoninDojo, veamos juntos cómo configurar este nodo.

## ¿Qué hardware elegir?

Para elegir la máquina que alojará y ejecutará RoninDojo, tienes varias opciones.

Como se explicó anteriormente, la opción más sencilla será pedir el Tanto, una máquina plug-and-play diseñada específicamente para este uso. Para pedir el tuyo, ve aquí: [https://shop.ronindojo.io/product-category/nodes/](https://shop.ronindojo.io/product-category/nodes/).

Dado que los equipos de RoninDojo producen código de código abierto, también es posible implementar RoninDojo en otras máquinas. Puedes encontrar las últimas versiones del asistente de instalación en esta página: [https://ronindojo.io/en/downloads.html](https://ronindojo.io/en/downloads.html), y las últimas versiones del código en esta página: [https://code.samourai.io/ronindojo/RoninDojo](https://code.samourai.io/ronindojo/RoninDojo).

Personalmente, lo he instalado en una Raspberry Pi 4 de 8GB y funciona perfectamente.

Sin embargo, ten en cuenta que los equipos de RoninDojo nos indican que a menudo hay problemas debido a la carcasa y al adaptador del SSD. Por lo tanto, no se recomienda utilizar una carcasa con un cable para el SSD de tu máquina. Es mejor utilizar una tarjeta de expansión de almacenamiento especialmente diseñada para tu placa base, como esta: [Carte d'extension de stockage Raspberry Pi 4](https://www.amazon.fr/Carte-dextension-stockage-Raspberry-Pi/dp/B07ZQV2J2N).

Aquí tienes un ejemplo de configuración para hacer tu propio nodo RoninDojo:

- Una Raspberry Pi 4.
- Una carcasa con un ventilador.
- Una tarjeta de expansión de almacenamiento compatible. \* Un cable de alimentación.
- Una tarjeta micro SD industrial de 16GB o más.
- Un SSD de 1TB o más.
- Un cable ethernet RJ45, se recomienda categoría 8.

## ¿Cómo instalar RoninDojo?

### Paso 1: Preparar la tarjeta micro SD de arranque.

Una vez que hayas montado tu máquina, podrás comenzar la instalación de RoninDojo. Para ello, comienza creando una tarjeta micro SD de arranque grabando la imagen de disco adecuada.

Inserta tu tarjeta micro SD en tu computadora personal y visita el sitio web oficial de RoninDojo para descargar la imagen de disco RoninOS: https://ronindojo.io/en/downloads.html.

Descarga la imagen de disco que corresponda a tu hardware. En mi caso, descargué la imagen "MANJARO-ARM-RONINOS-RPI4-22.03.IMG.XZ":

![Descargar imagen de disco RoninOS](assets/2.png)

Una vez descargada la imagen, verifica su integridad utilizando el archivo .SHA256 correspondiente. Te explico detalladamente cómo hacer esto en este artículo: ¿Cómo verificar la integridad de un software de Bitcoin en Windows?

Las instrucciones específicas para verificar la integridad de RoninOS también están disponibles en esta página en inglés: https://wiki.ronindojo.io/en/extras/verify.

Para grabar esta imagen en tu tarjeta micro SD, puedes utilizar un software como Balena Etcher que puedes descargar aquí: https://www.balena.io/etcher/.

Para hacerlo, selecciona la imagen en Etcher y flashea la en la tarjeta micro SD:

![Grabar imagen de disco con Etcher](assets/3.png)

Una vez que la operación haya terminado, puedes insertar la tarjeta micro SD de arranque en la Raspberry Pi y encender la máquina.

### Paso 2: Configurar RoninOS.

RoninOS es el sistema operativo de tu nodo RoninDojo, es una versión modificada de Manjaro, una distribución de Linux. Después de iniciar tu máquina y esperar unos minutos, podrás comenzar su configuración.

Para conectarte a distancia, deberás encontrar la dirección IP de tu máquina RoninDojo. Para ello, puedes, por ejemplo, acceder al panel de administración de tu router, o también puedes descargar un software como https://angryip.org/ para escanear tu red local y encontrar la IP de la máquina.

Una vez que hayas encontrado la IP, podrás tomar el control de tu máquina desde otra computadora conectada a la misma red local utilizando SSH.

Desde una computadora con MacOS o Linux, simplemente abre la terminal. Desde una computadora con Windows, puedes utilizar una herramienta especializada como Putty o directamente Windows PowerShell.

Una vez que hayas abierto la terminal, escribe el siguiente comando:

> ssh root@192.168.?.?

Simplemente reemplaza los dos signos de interrogación por la IP de tu RoninDojo encontrada anteriormente.

> Consejo: En una terminal, haz clic derecho para pegar un elemento.

A continuación, llegarás al panel de configuración de Manjaro. Elije la disposición correcta de tu teclado usando las flechas para cambiar el objetivo en la lista desplegable.

![Configuración del teclado de Manjaro](assets/4.png)

Elige un nombre de usuario y una contraseña para tu sesión. Utiliza una contraseña fuerte y haz una copia de seguridad segura. Puedes usar una contraseña más débil durante la instalación y luego cambiarla fácilmente con la opción de "copiar y pegar" en RoninUI. Esto te permitirá establecer una contraseña muy segura sin tener que pasar mucho tiempo escribiéndola manualmente durante la configuración de Manjaro.

![Configuración del nombre de usuario de Manjaro](assets/5.png)

A continuación, también se te pedirá que elijas una contraseña de root. Para la contraseña de root, introduce directamente una contraseña fuerte. No podrás cambiarla desde RoninUI. Asegúrate también de hacer una copia de seguridad de esta contraseña de root.

Luego, introduce tu localidad y tu zona horaria.

![Configuración de la zona horaria de Manjaro](assets/6.png)

![Configuración de la localidad de Manjaro](assets/7.png)

A continuación, elige un nombre de host.

![Configuración del nombre de host de Manjaro](assets/8.png)

Por último, verifica la información de configuración de Manjaro y confirma.

![Verificación de la información de configuración de ManjaroOS](assets/9.png)

### Paso 3: Descargar RoninDojo.

La configuración inicial de RoninOS se realizará. Una vez finalizada, como se muestra en la captura de pantalla anterior, la máquina se reiniciará. Espera unos momentos y luego ingresa el siguiente comando para volver a conectarte a tu máquina RoninDojo:

> ssh pseudo@192.168.?.?

Simplemente reemplaza "pseudo" por el nombre de usuario que elegiste anteriormente y los signos de interrogación por la IP de tu RoninDojo.

Luego, ingresa tu contraseña de usuario.

En la terminal, se verá así:

![Conexión SSH a RoninOS](assets/10.png)

Ahora estás conectado a tu máquina que actualmente solo tiene RoninOS. Ahora debes instalar RoninDojo en ella.

Descarga la última versión de RoninDojo ingresando el siguiente comando:

> git clone https://code.samourai.io/ronindojo/RoninDojo

La descarga se realizará rápidamente. En la terminal, se verá así:

![Clonación de RoninDojo](assets/11.png)

Espera a que termine la descarga, luego instala y accede a la interfaz de usuario de RoninDojo usando el siguiente comando:

> ~/RoninDojo/ronin

Se te pedirá que ingreses tu contraseña de usuario:

![Verificación de la contraseña del nodo Bitcoin](assets/12.png)

> Esta orden es necesaria solo la primera vez que accedes a tu RoninDojo. Después, para acceder a RoninCLI a través de SSH, simplemente debes ingresar la orden [SSH pseudo@192.168.?.?] reemplazando "pseudo" por tu nombre de usuario y colocando la IP de tu nodo. Se te pedirá tu contraseña de usuario.

Luego verás esta magnífica animación:

![Animación de inicio de RoninCLI](assets/13.png)

Finalmente llegarás a la interfaz de usuario CLI de RoninDojo.

### Paso 4: Instalar RoninDojo.

Desde el menú principal, accede al menú "System" utilizando las flechas de tu teclado. Utiliza la tecla Enter para confirmar tu elección.

![Navegación del menú RoninCLI hacia System](assets/14.png)

Luego ve al menú "System Setup & Install".

![Navegación del menú RoninCLI hacia la instalación del sistema de RoninDojo](assets/15.png)

Por último, marca "System Setup" y "Install RoninDojo" utilizando la barra espaciadora, luego selecciona "Aceptar" para iniciar la instalación.

![Confirmación de la instalación de RoninDojo](assets/16.png)

Deja que la instalación se realice tranquilamente. En mi caso, esto tomó aproximadamente 2 horas. Mantén tu terminal abierto durante la operación.

De vez en cuando, revisa tu terminal, se te pedirá que presiones una tecla en ciertos momentos de la instalación, como aquí por ejemplo:

![Instalación de RoninDojo en progreso](assets/17.png)

Al finalizar la instalación, verás que los diferentes contenedores se inician:

![Inicio de los contenedores del nodo](assets/18.png)

Luego tu nodo se reiniciará. Conéctate nuevamente a RoninCLI para el siguiente paso.

![Reinicio del nodo Bitcoin](assets/19.png)

### Paso 5: Descargar la cadena de prueba de trabajo y acceder a RoninUI.

Una vez finalizada la instalación, tu nodo comenzará a descargar la cadena de prueba de trabajo de Bitcoin. Esto se conoce como IBD (Initial Block Download). Por lo general, esto lleva entre 2 y 14 días, dependiendo de tu conexión a internet y tu dispositivo.

Puedes seguir el progreso de la descarga de la cadena accediendo a la interfaz web de RoninUI.

Para acceder desde una red local, ingresa en la barra de direcciones de tu navegador:

- Directamente la dirección IP de tu máquina (192.168.?.?)

- O bien: ronindojo.local

Asegúrate de desactivar tu VPN si estás utilizando uno.

### Posible complicación

Si no puedes acceder a RoninUI desde tu navegador, verifica el correcto funcionamiento de la aplicación desde tu Terminal conectado a tu nodo a través de SSH. Conéctate al menú principal siguiendo los pasos anteriores:

- Escribe: SSH pseudo@192.168.?.? reemplazando con tus credenciales.

- Ingresa tu contraseña de usuario.
  Une fois on the main menu, go to:
  > RoninUI > Restart

If the application restarts correctly, it is a problem with the connection from your browser. Make sure you are not using a VPN and check that you are connected to the same network as your node.

If the restart gives an error, try updating the operating system and then reinstalling RoninUI. To update the OS:

> System > Software Updates > Update Operating System

Once the update and restart are complete, reconnect to your node via SSH and reinstall RoninUI:

> RoninUI > Re-install

After downloading RoninUI again, try to connect via your browser to RoninUI.

> Tip: If you accidentally exit RoninCLI and find yourself on the Manjaro terminal, simply enter the command "ronin" to return directly to the main menu of RoninCLI.

### Web log in

You can also log in to the RoninUI web interface from any network using Tor. To do this, retrieve the Tor address of your RoninUI from RoninCLI:

> Credentials > Ronin UI

Retrieve the Tor address ending in .onion and then connect to Ronin UI by entering this address in your Tor browser. Be careful not to leak your different credentials, as they are sensitive information.

![Web interface for logging into RoninUI](assets/20.png)

Once connected, you will be asked for your user password. It is the same password you use to connect via SSH.

![RoninUI web interface management panel](assets/21.png)

We can observe the progress of the IBD. Be patient, you are in the process of retrieving all the transactions made on Bitcoin since January 3, 2009.

After downloading the entire blockchain, the indexer will compact the database. This operation takes about 12 hours. You can also track its progress under "Indexer" on RoninUI.

Your RoninDojo node will be fully functional after this:

![Indexer synchronized at 100% functional node](assets/22.png)

If you want to change the user password to a stronger one, you can do so now from the "Settings" tab. On RoninDojo, there is no additional security layer, so I advise you to choose a really strong password and take care of its backup.

## How to use RoninDojo?

Once the chain is downloaded and compacted, you can start enjoying the services offered by your new RoninDojo node. Let's see how to use them.

### Connecting wallet software to electrs.

La primera utilidad de su nodo recién instalado y sincronizado será difundir sus transacciones a la red de Bitcoin. Seguramente querrá conectar sus diferentes software de gestión de carteras.

Puede hacer esto a través de Electrum Rust Server (electrs). La aplicación normalmente está preinstalada en su nodo RoninDojo. Si no es así, puede instalarla manualmente desde la interfaz RoninCLI.

Simplemente vaya a:

> Aplicaciones > Administrar aplicaciones > Instalar Electrum Server

Para obtener la dirección Tor de su Electrum Server, desde el menú RoninCLI, vaya a:

> Credenciales > Electrs

Solo tendrá que ingresar el enlace en .onion en su software de cartera. Por ejemplo, en Sparrow Wallet, simplemente vaya a la pestaña:

> Archivo > Preferencias > Servidor

En el tipo de servidor, seleccione "Private Electrum", luego ingrese la dirección Tor de su Servidor Electrum en el campo correspondiente. Finalmente, haga clic en "Probar conexión" para probar y guardar su conexión.

![Interface de connexion de Sparrow Wallet à un electrs](assets/23.png)

### Conectar sus software de carteras a Samourai Dojo.

En lugar de usar Electrs, también puede usar Samourai Dojo para conectar su cartera de software compatible a su nodo RoninDojo. Por ejemplo, Samourai Wallet ofrece esta opción.

Para hacer esto, simplemente escanee el código QR de conexión de su Dojo. Para acceder a él desde RoninUI, haga clic en la pestaña "Panel de control" y luego en el botón "Administrar" en el cuadro de su Dojo. Luego podrá ver los códigos QR de conexión a su Dojo y a BTC-RPC Explorer. Para mostrarlos, haga clic en "Mostrar valores".

![Récupération du QRcode de connexion au Dojo](assets/24.png)

Para conectar su cartera Samourai Wallet a su Dojo, deberá escanear este código QR durante la instalación de la aplicación:

![Connexion à Dojo depuis l'application Samourai Wallet](assets/25.png)

### Utilizar su propio Explorer Mempool.

Herramienta esencial para los Bitcoiners, el explorador le permite verificar diferentes información sobre la cadena de Bitcoin. Con Mempool, por ejemplo, puede verificar en tiempo real las tarifas aplicadas por otros usuarios para ajustar las suyas. También puede verificar el estado de confirmación de una de sus transacciones o ver el saldo de una dirección.

Estas herramientas de explorador pueden exponerlo a riesgos de pérdida de confidencialidad y lo obligan a confiar en la base de datos de un tercero. Cuando utiliza esta herramienta en línea sin pasar por su propio nodo:

- Corre el riesgo de filtrar información sobre su cartera.

- Confía en el administrador del sitio web para la cadena de prueba de trabajo que aloja.
  Para evitar estos riesgos, puedes utilizar tu propia instancia de Mempool en tu nodo a través de la red Tor. Con esta solución, no solo preservas tu privacidad al utilizar el servicio, sino que también ya no necesitas confiar en un proveedor ya que consultas tu propia base de datos.

Para ello, comienza por instalar Mempool Space Visualizer desde RoninCLI:

> Aplicaciones > Administrar aplicaciones > Instalar Mempool Space Visualizer

Una vez instalado, obtén el enlace a tu Mempool. La dirección Tor te permitirá acceder a ella desde cualquier red. De la misma manera, obtenemos este enlace a través de RoninCLI:

> Credenciales > Mempool

![Récupération adresse Tor Mempool](assets/26.png)

Simplemente ingresa tu dirección Mempool Tor en el navegador Tor para disfrutar de tu propia instancia de Mempool, basada en tus propios datos. Te recomiendo agregar esta dirección Tor a tus favoritos para poder acceder a ella más rápidamente. También puedes crear un acceso directo en tu escritorio.

![Interface Mempool Space](assets/27.png)

Si aún no tienes el navegador Tor, puedes descargarlo aquí: https://www.torproject.org/download/

También puedes acceder desde tu teléfono inteligente instalando Tor Browser y luego ingresando la misma dirección. Desde cualquier lugar, podrás ver el estado de la cadena de Bitcoin utilizando tu propio nodo.

### Utilizar Whirlpool CLI.

Tu nodo RoninDojo también incluye WhirlpoolCLI, una interfaz de línea de comandos remota que permite automatizar las mezclas de Whirlpool.

Cuando realizas un CoinJoin con la implementación de Whirlpool, la aplicación que estás utilizando debe permanecer abierta para poder ejecutar mezclas y remezclas. Este proceso puede resultar tedioso para el usuario que busca tener conjuntos anónimos elevados, ya que el dispositivo que aloja la aplicación con Whirlpool debe permanecer encendido constantemente. En pocas palabras, esto significa que si deseas comprometer tus UTXO en remezclas las 24 horas del día, los 7 días de la semana, deberás dejar tu computadora personal o tu teléfono encendidos constantemente con la aplicación abierta.

Una solución a esta limitación es utilizar WhirlpoolCLI en una máquina destinada a estar encendida constantemente, como por ejemplo un nodo Bitcoin. Gracias a esto, nuestros UTXO podrán remezclarse las 24 horas del día y los 7 días de la semana sin necesidad de dejar otra máquina que no sea nuestro nodo Bitcoin en funcionamiento.
'WhirlpoolCLI se utiliza junto con WhirlpoolGUI, una interfaz gráfica que se instala en una computadora personal para facilitar la gestión de Coinjoins. Explico en detalle cómo configurar Whirlpool CLI con su propio dojo en este artículo: https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin#:~:text=dans%20cette%20partie.-,Tutoriel%20%3A%20Whirpool%20CLI%20sur%20Dojo%20et%20Whirlpool%20GUI.,-Si%20vous%20souhaitez
Para obtener más información sobre Coinjoin en general, explico todo en este artículo: https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin

### Utilizar Whirlpool Stat Tool.

Después de realizar CoinJoin con Whirlpool, es posible que desee saber concretamente cuál es el nivel de privacidad de sus UTXO mezclados. Whirlpool Stat Tool le permite hacer esto fácilmente. Con esta herramienta, podrá calcular la puntuación prospectiva y la puntuación retrospectiva de sus UTXO mezclados. Para obtener más información sobre el cálculo de estos conjuntos anónimos y su funcionamiento, le recomiendo que lea esta parte: https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin#:~:text=perdre%20en%20confidentialit%C3%A9.-,Anon%20Sets.,-Comme%20expliqu%C3%A9%20pr%C3%A9c%C3%A9demment

La herramienta está preinstalada en su RoninDojo. Por el momento, solo está disponible desde RoninCLI. Para iniciarlo desde el menú principal, vaya a:

> Samourai Toolkit > Whirlpool Stat Tool

Las instrucciones de uso se mostrarán. Una vez que haya terminado, presione cualquier tecla para acceder a las líneas de comando:

![Accueil logiciel Whirlpool Stats Tool](assets/28.png)

Verá que se muestra el terminal:

> wst#/tmp>

Para salir de esta interfaz y volver al menú RoninCLI, simplemente escriba el comando:

> quit

Para comenzar, vamos a configurar el proxy en Tor para poder extraer los datos de OXT de manera confidencial. Escriba el comando:

> socks5 127.0.0.1:9050

A continuación, descargue los datos del grupo que contiene su transacción:

> download 0001
>
> Reemplace 0001 con el código de denominación del grupo que le interese.

Los códigos de denominación son los siguientes en WST:

- Grupo de 0,5 bitcoins: 05

- Grupo de 0,05 bitcoins: 005

- Grupo de 0,01 bitcoins: 001

- Grupo de 0,001 bitcoins: 0001

![Téléchargement des données de la pool 0001 depuis OXT](assets/29.png)

Una vez que se hayan descargado los datos, cárguelos con el comando:

> load 0001
>
> Reemplace 0001 con el código de denominación del grupo que le interese.'
> '![Chargement des données de la pool 0001](assets/30.png)
> Deje que se carguen los datos, esto puede tomar algunos minutos. Después de cargar los datos, escriba el comando score seguido de su TXID (identificador de transacción) para obtener sus conjuntos Anon:

> score TXID
>
> Reemplace TXID con el identificador de su transacción.

![Impression des scores prospectifs et rétrospectifs de la TXID donnée](assets/31.png)

WST mostrará primero el puntaje retrospectivo (métricas retrospectivas) y luego el puntaje prospectivo (métricas prospectivas). Además de los puntajes de los conjuntos Anon, WST también le proporciona la tasa de difusión de su salida en el grupo en función del conjunto Anon.

Tenga en cuenta que el puntaje prospectivo de su UTXO se calcula a partir del TXID de su mezcla inicial, no del último mezcla. Por el contrario, el puntaje retrospectivo de un UTXO se calcula a partir del TXID del último ciclo.

Una vez más, si no entiende estos conceptos de conjuntos Anon, le recomiendo que lea esta parte de mi artículo sobre Coinjoin en el que explico todo en detalle con diagramas: https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin#:~:text=perdre%20en%20confidentialit%C3%A9.-,Anon%20Sets.,-Comme%20expliqu%C3%A9%20pr%C3%A9c%C3%A9demment

### Utilizar la calculadora Boltzmann.

La calculadora Boltzmann es una herramienta que le permite calcular fácilmente diversas métricas avanzadas en una transacción de Bitcoin, incluido su nivel de entropía. Todos estos datos le permitirán poner números al nivel de confidencialidad de una transacción y detectar posibles errores. Esta herramienta está preinstalada en su nodo RoninDojo.

Para acceder a ella desde RoninCLI, conéctese a través de SSH y vaya al menú:

> Samourai Toolkit > Boltzmann Calculator

Antes de explicar cómo usarlo en RoninDojo, explicaré qué representan estas métricas, cómo se calculan y para qué sirven.

Estos indicadores se pueden utilizar para cualquier transacción de Bitcoin, pero son particularmente interesantes para estudiar la calidad de una transacción Coinjoin.

1. El primer indicador calculado por este software es el número de combinaciones posibles. Se muestra en la calculadora como "nb combinations". Dado los valores de UTXO, este indicador representa el número de asignaciones posibles de las entradas a las salidas.

> Si no está familiarizado con el término "UTXO", le recomiendo que lea este breve artículo: Mecanismo de una transacción de Bitcoin: UTXO, inputs y outputs.'
> En otras palabras, este indicador representa la cantidad de interpretaciones posibles para una transacción dada. Por ejemplo: un Coinjoin de estructura Whirlpool 5x5 tendrá un número de combinaciones posibles igual a 1496:
> ![Schéma d'une transaction Coinjoin sur kycp.org](assets/32.png)

Crédito: https://kycp.org/#/fe5e5abab7ea452f87603f7ebc2fa4e77380eafcc927e1cb51e1a72401ab073d

2. El segundo indicador calculado es la entropía de una transacción ("Entropy"). Dado que el número de combinaciones posibles puede ser muy alto para una transacción, se puede optar por utilizar la entropía. La entropía representa el logaritmo binario del número de combinaciones posibles. Su fórmula es la siguiente para:

- E: la entropía de la transacción.

- C: el número de combinaciones posibles para la transacción.

> E = log2(C)

En matemáticas, el logaritmo binario (base 2) es la función recíproca de la función potencia de 2. En otras palabras, el logaritmo binario de x es la potencia a la que el número 2 debe elevarse para obtener el valor x.

Así:

> E = log2(C)
> C = 2^E

Este indicador se expresa en bits. Por ejemplo, aquí está el cálculo de la entropía de una transacción Coinjoin de estructura Whirlpool 5x5, con el número de combinaciones posibles igual a 1496 como se mencionó anteriormente:

> C = 1496
>
> E = log2(1496)
>
> E = 10.5469 bits

Esta transacción Coinjoin tiene una entropía de 10.5469 bits, lo cual es muy bueno.

Cuanto más alto sea este indicador, más interpretaciones diferentes de la transacción habrá, y por lo tanto, más confidencial será la transacción.

Tomemos otro ejemplo. Aquí hay una transacción "clásica" que tiene una entrada y dos salidas:

![Transaction schéma bitcoin sur oxt.me](assets/34.png)

Crédito: https://oxt.me/graph/transaction/tiid/9815286

Esta transacción solo tiene una única interpretación posible:

> [(inp 0) > (Outp 0 ; Outp 1)]

Por lo tanto, su entropía será igual a 0:

> C = 1
>
> E = log2(C)
>
> E = 0

3. El tercer indicador devuelto por el calculador Boltzmann es la eficiencia de la Tx llamada "Wallet Efficiency". Este indicador simplemente permite comparar la transacción de entrada con la mejor transacción posible en la misma configuración.
   Se va a introducir el concepto de entropía máxima que representa la entropía más alta alcanzable para una estructura de transacción dada. Por ejemplo, la estructura de Coinjoin de tipo Whirlpool 5x5 tendrá una entropía máxima igual a 10.5469. Por lo tanto, el indicador de eficiencia compara esta entropía máxima con la entropía real de la transacción de entrada. Su fórmula es la siguiente para:

- ER: Entropía real expresada en bits.

- EM: Entropía máxima con la misma estructura expresada en bits.

- Ef: Eficiencia expresada en bits.

> Ef = ER - EM
>
> Ef = 10.5469 - 10.5469
>
> Ef = 0 bits

Este indicador también se expresa en porcentaje, por lo que su fórmula es la siguiente:

- CR: Número de combinaciones posibles reales.

- CM: Número de combinaciones posibles como máximo con la misma estructura.

- Ef: Eficiencia expresada en porcentaje.

> Ef = CR/CM
>
> Ef = 1496/1496
>
> Ef = 100%

Una eficiencia del 100% significa que esta transacción tiene la máxima privacidad posible en comparación con su estructura.

4. El cuarto indicador calculado es la densidad de la entropía ("Entropy Density"). Permite relacionar la entropía con cada entrada o salida. Por lo tanto, se puede utilizar este indicador para comparar la eficiencia entre varias transacciones de diferentes tamaños.

Su cálculo es muy sencillo, se divide la entropía de la transacción entre el número de inputs y outputs presentes en ella. Por ejemplo, para un Coinjoin de tipo Whirlpool 5x5 tendremos:

    ED: Densidad de la entropía expresada en bits.

    E: Entropía de la transacción expresada en bits.

    T: número total de inputs y outputs en la transacción.

T = 5 + 5 = 10
ED = E / T
ED = 10.5469 / 10
ED = 1.054 bits

La quinta información proporcionada por el calculador Boltzmann es la tabla de probabilidades de enlaces entre las entradas y las salidas. Esta tabla simplemente le dará la probabilidad (puntuación de Boltzmann) de que una entrada dada corresponda a una salida dada.

Si retomamos nuestro ejemplo con un Coinjoin Whirlpool, la tabla de probabilidades será:

| Input | Output 0 | Output 1 | Output 2 | Output 3 | Output 4 |
| ----- | -------- | -------- | -------- | -------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0     | 34%      | 34%      | 34%      | 34%      | 34%      |
| 1     | 34%      | 34%      | 34%      | 34%      | 34%      |
| 2     | 34%      | 34%      | 34%      | 34%      | 34%      |
| '     | 3        | 34%      | 34%      | 34%      | 34%      | 34% |     | 4   | 34% | 34% | 34% | 34% | 34% |

Aquí se puede ver que cada entrada tiene la misma probabilidad de estar vinculada a cada salida.

Sin embargo, si tomamos el ejemplo de una transacción con una entrada y dos salidas, entonces sería:

| Entrada | Salida 0 | Salida 1 |
| ------- | -------- | -------- |
| 0       | 100%     | 100%     |

En este ejemplo se puede ver que la probabilidad de que cada salida provenga de la entrada 0 es del 100%.

Cuanto más baja sea esta probabilidad, más confidencialidad habrá.

6. La sexta información que se calcula es el número de enlaces deterministas. También se proporcionará la proporción de enlaces deterministas. Este indicador destaca el número de enlaces entre las entradas y salidas de la transacción dada que tienen una probabilidad del 100%, es decir, que son indiscutibles.

La proporción permite indicar el número de enlaces deterministas en la transacción en relación con el número total de enlaces.

Por ejemplo, una transacción Coinjoin Whirlpool no tiene ningún enlace determinista entre las entradas y salidas. El indicador será igual a cero y la proporción también será del 0%.

Sin embargo, para la segunda transacción estudiada (1 entrada y 2 salidas), el indicador es igual a 2 y la proporción es del 100%.

Por lo tanto, si este indicador es igual a cero, indica una buena confidencialidad.

Ahora que hemos estudiado los indicadores, veamos cómo calcularlos utilizando este software. Desde RoninCLI, vaya al menú:

> Samourai Toolkit > Boltzmann Calculator

![Página de inicio del software Boltzmann Calculator](assets/35.png)

Una vez que se haya iniciado el software, ingrese el identificador de la transacción que desea estudiar. Puede ingresar varias transacciones a la vez separándolas con una coma y luego presionar Enter:

![Ingrese un TXID para estudiar en Boltzmann Calculator](assets/36.png)

El calculador le devolverá todos los indicadores que hemos visto anteriormente:

![Impresión de los datos de Boltzmann Calculator para este TXID](assets/37.png)

Escriba el comando "Quit" para salir del software y volver al menú de RoninCLI.

Para obtener más información sobre el calculador Boltzmann, le recomiendo que lea estos artículos:

- https://medium.com/@laurentmt/introducing-boltzmann-85930984a159

- https://gist.github.com/LaurentMT/e758767ca4038ac40aaf

### Conectar Bisq.

Bisq es una plataforma de intercambio que le permite realizar compras y ventas de bitcoins de igual a igual. Se utiliza con un software de escritorio que se ejecuta a través de Tor y que permite intercambiar bitcoins sin necesidad de proporcionar su identidad.
Bisq asegura el intercambio peer-to-peer mediante un sistema de multi-firma 2/2. Puede utilizar este software con su propio nodo RoninDojo para optimizar la privacidad de sus intercambios y confiar en los datos del blockchain de su propio nodo.
Para descargar el software Bisq, visite su sitio web oficial: https://bisq.network/

Para familiarizarse con el software, le recomiendo que lea esta página: https://bisq.network/getting-started/

Para obtener el enlace de conexión desde su RoninDojo, deberá conectarse a RoninCLI a través de SSH. Luego vaya al menú:

> Aplicaciones > Administrar aplicaciones

Ingrese su contraseña y luego marque la casilla con la tecla de espacio:

> [ ] Habilitar conexión Bisq

Confirme su elección. Deje que su nodo se instale y luego obtenga la dirección Tor V3 desde:

> Credenciales > Bitcoind

Copie la dirección debajo de "Bitcoin Daemon".

También puede obtener su dirección Bitcoind Tor V3 desde la interfaz RoninUI simplemente haciendo clic en "Administrar" en la casilla "Bitcoin Core" desde el "Tablero":

![Obtener dirección TorV3 Bitcoin Daemon en RoninUI](assets/38.png)

Para conectar su nodo desde Bisq, vaya al menú:

> Configuración > Información de red

![Acceder a la interfaz de conexión del nodo desde el software Bisq](assets/39.png)

Haga clic en el globo "Usar nodos Bitcoin Core personalizados". Luego ingrese su dirección Bitcoin TorV3 en el campo provisto para ello, con el ".onion" pero sin el "http://".

![Campo para ingresar la dirección TorV3 de su nodo en el software Bisq](assets/40.png)

Reinicie el software Bisq. Su nodo ahora está conectado a su Bisq.

### Otras características.

Su nodo RoninDojo también incluye otras características básicas. Tiene la posibilidad de escanear información específica para asegurarse de tenerla en cuenta.

Por ejemplo, a veces es posible que su billetera conectada a su RoninDojo no encuentre los bitcoins que le pertenecen. El saldo es 0 aunque esté seguro de que tiene bitcoins en esta billetera. Hay muchas posibles causas a tener en cuenta, incluido un error en las rutas de derivación, y entre ellas también es posible que su nodo no esté observando sus direcciones.

Para solucionarlo, puede verificar que su nodo esté rastreando su xpub con la herramienta "xpub tool". Para acceder a ella desde RoninUI, vaya al menú:

> Mantenimiento > Herramienta XPUB

Ingrese la xpub que está causando problemas y haga clic en "Verificar" para verificar esta información.

![Herramienta XPUB desde RoninUI](assets/41.png)

Si su xpub está siendo rastreada correctamente por el nodo, verá esto:

![Herramienta XPUB resultado favorable del análisis](assets/42.png)
Verifique que todas las transacciones aparezcan correctamente. También verifique que el tipo de derivación coincida con el de su billetera. Aquí podemos ver que el nodo interpreta esta xpub como una derivación BIP44. Si este tipo de derivación no coincide con el de su billetera, haga clic en el botón "Retype" y seleccione BIP44/BIP49/BIP84 según su elección:
![Changer le type de dérivation de la xpub étudiée depuis RoninUI](assets/43.png)

Si su xpub no está rastreada por su nodo, verá esta pantalla que le invita a importarla:
![Importer une xpub avec outil XPUB Tool sur RoninUI](assets/44.png)

También puede utilizar otras herramientas de mantenimiento:

- Transaction Tool: Le permite observar los detalles de una transacción específica.
- Address Tool: Le permite verificar si una dirección específica está siendo rastreada por su Dojo.
- Rescan Blocks: Obliga a su nodo a volver a escanear un rango de bloques seleccionado.

También encontrará en RoninUI la herramienta "Push Tx". Le permite difundir una transacción firmada a la red de Bitcoin. Esta debe ingresarse en formato hexadecimal:
![Outil de diffusion d'une transaction signée depuis RoninUI](assets/45.png)

## Conclusion.

Hemos podido ver cómo instalar y utilizar esta magnífica herramienta que es RoninDojo. Es una excelente opción para ejecutar su propio nodo de Bitcoin. Es una solución estable que integra y mantiene actualizadas todas las herramientas esenciales para un Bitcoiner.

Si no le teme al uso de la terminal y no necesita herramientas relacionadas con la Lightning Network, entonces RoninDojo puede ser de su agrado.

Si puede hacerlo, considere hacer una donación a los desarrolladores que producen estos software de código abierto de forma gratuita para usted: https://donate.ronindojo.io/

Para obtener más información sobre RoninDojo, le recomiendo que consulte los enlaces en mis recursos externos a continuación.

### Para ir más allá:

- Comprender y utilizar CoinJoin en Bitcoin.
- Las funciones hash - extracto del libro electrónico Bitcoin Démocratisé 1.
- Todo sobre la frase de contraseña de Bitcoin.

### Recursos externos:

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
