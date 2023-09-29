---
name: GrapheneOS

description: Tutorial de Graphene OS
---

# Graphene OS

> "[GrapheneOS](https://grapheneos.org/) es un sistema operativo móvil centrado en la privacidad y la seguridad, con compatibilidad con aplicaciones de Android, desarrollado como un proyecto de código abierto sin fines de lucro."

GrapheneOS, fundado originalmente en 2014 como 'CopperheadOS', se basa en el código tradicional de Android (AOSP), pero con muchos cambios y mejoras orientados a mejorar la privacidad y la seguridad del usuario. GrapheneOS pone al usuario en control de su teléfono, no de las grandes empresas tecnológicas.

### Índice:

- Introducción
- Preparación
- Instalación
- Alternativas de aplicaciones
- Desventajas
- Información útil

Guía por https://github.com/BitcoinQnA/Bitcoiner.Guide/blob/main/grapheneos.md

## ¿Por qué usar GrapheneOS?

Los teléfonos modernos son dispositivos de seguimiento y recolección de datos de 500 a 1000 dólares. Cada aspecto de nuestra vida pasa por ellos y, desafortunadamente, gran parte de estos datos se comparte con terceros de alguna forma u otra.
GrapheneOS está construido específicamente para reducir esta compartición de datos y mejorar la seguridad de su dispositivo frente a posibles vectores de ataque. No existe tal cosa como una cuenta de GrapheneOS. No necesitas una para descargar aplicaciones o interactuar con el sistema operativo. En pocas palabras, tú no eres el producto.

GrapheneOS proporciona seguridad adicional a tu experiencia de Android a través de algunos principios básicos.

1. **Reducción de superficie de ataque** - Eliminar código innecesario (o software innecesario).
2. **Prevención de exposición a vulnerabilidades** - Permitir al usuario suficiente granularidad para elegir los compromisos con los que se sienten cómodos.
3. **Contención de sandbox** - GrapheneOS fortalece los sandbox existentes de Android, limitando aún más la capacidad de cada aplicación para comunicarse con el resto de tu teléfono.

Obtén más información sobre los detalles técnicos del conjunto de funciones de GrapheneOS [aquí](https://grapheneos.org/features).

### Facilitando la transición

Si has estado inmerso en el ecosistema de Google o Apple durante años, la idea de perder toda esa comodidad de la noche a la mañana puede ser aterradora. Pero con decisiones cuidadosamente consideradas sobre la instalación de aplicaciones (que se tratarán más adelante), gran parte de esta dificultad esperada puede reducirse o eliminarse.

Aunque las alternativas están mejorando, el pensamiento de un cambio así todavía puede resultar desalentador. Si te encuentras en esta situación, mi mejor consejo es utilizar tu nuevo dispositivo GrapheneOS junto con tu teléfono actual durante un tiempo. A partir de ahí, puedes ir reduciendo gradualmente el uso de 2-3 aplicaciones por semana hasta que solo utilices tu dispositivo GrapheneOS.

Si adoptas este enfoque, sé estricto contigo mismo y corta tu dependencia de las alternativas vigiladas lo más rápido posible. Los humanos somos perezosos y a menudo elegimos el camino de menor resistencia. Recuerda por qué hiciste el cambio en primer lugar.

**En lugar de pagar con tus datos personales, elegiste pagar con tu tiempo y, a veces, con tu dinero ganado con esfuerzo (dependiendo de las aplicaciones alternativas que instales).**

## Empezando

Actualmente, GrapheneOS solo está disponible para la gama de teléfonos [Google Pixel](https://grapheneos.org/faq#supported-devices) _(irónicamente)_. Sin embargo, esto no es sin una buena razón. Los Pixel ofrecen la mejor seguridad basada en hardware para complementar el trabajo realizado para fortalecer el sistema operativo. Esto incluye cosas como aislamientos de componentes específicos y arranque verificado.

### Elegir un dispositivo

Al elegir el Pixel en el que deseas instalar GrapheneOS, asegúrate de verificar durante cuánto tiempo el dispositivo seguirá recibiendo [actualizaciones de seguridad](https://support.google.com/pixelphone/answer/4457705?hl=en#zippy=%2Cpixel-xl-a-a-g-a-g) por defecto.
Al momento de escribir esto, el Pixel 6a es el modelo más económico disponible con un buen soporte a largo plazo, garantizado hasta julio de 2027. Si eliges este modelo, la desbloqueo OEM no funcionará con la versión del sistema operativo de fábrica. Debes actualizarlo a la versión de junio de 2022 o posterior a través de una actualización por aire. Después de actualizarlo, también deberás restablecer el dispositivo a los valores de fábrica para solucionar el desbloqueo OEM. Todos los demás modelos que estén desbloqueados por el operador estarán listos para GrapheneOS directamente desde la caja.

Al elegir un dispositivo, también debes asegurarte de comprar una versión desbloqueada. Ciertos operadores como Verizon envían sus unidades con el gestor de arranque bloqueado, lo que impide por completo el siguiente proceso.

### Instalación de GrapheneOS

El [instalador web](https://grapheneos.org/install/web) de GrapheneOS hace que todo el proceso sea muy sencillo y puede ser completado por cualquier persona en menos de 10 minutos.
Las siguientes instrucciones son una versión resumida tomada del enlace anterior.

Todo lo que necesitas tener a mano es:

- El Pixel
- Un cable USB para conectar el teléfono a tu computadora
- Una computadora para ejecutar un navegador web (cualquier navegador basado en Chromium: Chrome, Edge, Brave, etc.)

1. El primer paso es ir a **Configuración** > **Acerca del teléfono** y tocar repetidamente el número de compilación hasta que veas que se activa **"Modo desarrollador"**.
2. A continuación, ve a **Configuración** > **Sistema** > **Opciones de desarrollador** y habilita **"Desbloqueo OEM"**.
3. Reinicia el dispositivo y mantén presionado el botón de volumen hacia abajo mientras el teléfono se enciende nuevamente.
4. Conecta el teléfono a tu computadora portátil y, si se solicita autorización, permite la conexión.
5. En la página del instalador web, haz clic en **"Desbloquear el gestor de arranque"**.
6. Luego verás que cambian las opciones del teléfono. Usa el botón de volumen para cambiar la selección a `desbloquear` y usa el botón de encendido para aceptar.
7. A continuación, haz clic en **"Descargar versión"** en la página del instalador web.
8. Una vez que se haya descargado por completo, pasa al siguiente paso y haz clic en **"Flashear versión"**. Esto tomará uno o dos minutos y no necesitas tocar el teléfono en absoluto.
9. Por último, pasa al siguiente paso del instalador web y haz clic en **"Bloquear el gestor de arranque"**. Deberás cambiar la selección y confirmar con el botón de encendido de la misma manera que hiciste anteriormente en el proceso.
10. Cuando veas la palabra `Iniciar`, confírmala con el botón de encendido y el dispositivo se iniciará en tu nuevo sistema operativo sin Google.

![imagen](assets/2.png)

_Después del inicio y la configuración inicial, es recomendable desactivar el desbloqueo OEM desde Configuración > Sistema > Opciones de desarrollador._

_También puedes considerar dar el paso adicional, opcional pero recomendado, de verificar la instalación a través de la aplicación Auditor. Necesitarás un teléfono Android separado con la aplicación instalada para completar este paso. Las instrucciones se pueden encontrar [aquí](https://attestation.app/tutorial)._

![video](https://www.youtube.com/embed/L1KZWjZVnAw)

Si esos simples pasos parecen demasiado complicados, puedes considerar comprar un Pixel con el software GrapheneOS [preinstalado](https://ronindojo.io/en/roninmobile). Solo ten en cuenta que estás depositando una pequeña cantidad de confianza en el proveedor.

### Aplicaciones preinstaladas

Ahora que estás configurado, es posible que notes lo básico que parece GrapheneOS después de la primera instalación. De forma predeterminada, tendrás estas aplicaciones instaladas:

![image](assets/3.png)

Las únicas dos con las que es posible que no estés familiarizado son 'Auditor' y 'Vanadium'.

- La [aplicación Auditor](https://play.google.com/store/apps/details?id=app.attestation.auditor) utiliza características de seguridad basadas en hardware para validar la identidad de un dispositivo junto con la autenticidad y la integridad del sistema operativo. Verificará que el dispositivo esté ejecutando el sistema operativo original con el gestor de arranque bloqueado y que no se haya producido ninguna manipulación del sistema operativo.
- [Vanadium](https://github.com/GrapheneOS/Vanadium) es una variante del navegador web Chromium con mayor privacidad y seguridad.

## Personalización

La configuración del teléfono es algo personal, pero aquí hay algunos de los primeros elementos que cambio al instalar GrapheneOS para sentirme más cómodo.

### Establecer un fondo de pantalla y actualizar el tema

Ve a Configuración > Fondo de pantalla y estilo. Desde aquí:

- Actualiza los fondos de pantalla de la pantalla de inicio y bloqueo con imágenes descargadas de la web.
- Elige los colores de acento utilizados en toda la interfaz de usuario.
- Habilita el tema oscuro.

### Mostrar el porcentaje de batería

Ve a **Configuración** > **Batería**, luego habilita **Mostrar el porcentaje de batería** en la barra de estado.

### Importar contactos

**Desde otro teléfono Android** - Ve a la aplicación de Contactos y busca la opción Exportar a VCF.

**Desde iOS** - Utiliza una aplicación como Export Contact y utiliza la opción de exportar 'vCard' para exportar un archivo VCF.
Una vez que tengas el archivo VCF, puedes transferirlo a tu dispositivo GrapheneOS con una opción de almacenamiento externo como una tarjeta microSD o una unidad USB. Si no tienes ninguna de esas opciones a mano, puedes optar por compartirlo a través de una de las muchas aplicaciones que se enumeran a continuación.

![image](assets/4.png)

## Aplicaciones alternativas

¡Para hacer que tu teléfono sea útil, querrás instalar algunas aplicaciones! Las opciones que se mencionan a continuación están incluidas porque las he utilizado personalmente o porque reciben fuertes recomendaciones de la comunidad de privacidad en general. Hay muchas otras excelentes alternativas disponibles que no se mencionan, y [Awesome Privacy](https://awesome-privacy.xyz) ofrece una lista increíblemente extensa de aplicaciones para preservar la privacidad para todo tipo de dispositivos.

El hecho de que una aplicación sea Software Libre y de Código Abierto (FOSS) no significa que esté libre de posibles filtraciones de privacidad. Utiliza [Exodus](https://reports.exodus-privacy.eu.org/en/) para ver cómo funcionan tus aplicaciones preferidas en sus auditorías de privacidad.

### F-Droid

[F-Droid](https://f-droid.org/) es un catálogo instalable de aplicaciones FOSS para Android. El cliente facilita la navegación, instalación y actualización de aplicaciones en tu dispositivo. Vale la pena mencionar que las actualizaciones a través de F-Droid a veces pueden ser más lentas que con otras tiendas de aplicaciones. Esto depende principalmente de si la aplicación se encuentra en el repositorio principal de F-Droid o en uno personalizado.

Para instalar F-Droid, simplemente ve a su sitio web a través de un navegador en tu teléfono GrapheneOS y toca descargar. Esto descargará un archivo `.apk`. Luego se te preguntará si deseas instalar la aplicación.

Además de las aplicaciones que se encuentran dentro del repositorio predeterminado en F-Droid, muchos proyectos de código abierto también alojarán su propio repositorio que se puede agregar en la configuración de la aplicación F-Droid. Si este es el caso, el proyecto en cuestión te guiará a través de los pasos muy sencillos requeridos para lograr esto en su sitio web.

![image](assets/5.png)

### Aurora Store

[Aurora Store](https://auroraoss.com/) es una versión de código abierto del Google Play Store. Aurora se ve y se siente muy similar a la tienda Play Store tradicional y te permite descargar y actualizar cualquier aplicación que normalmente encontrarías a través de la opción de Google.

La característica destacada de Aurora es el inicio de sesión anónimo. Esto significa que puedes descargar cualquiera de tus aplicaciones favoritas que no están disponibles a través de F-Droid o APK directo, sin tener que iniciar sesión en tu cuenta de Google.

Antes de apresurarte a hacer de esto tu opción de instalación predeterminada, recuerda que muchas de las aplicaciones de las que estamos tratando de alejarnos se instalaron desde la Play Store. El hecho de que sean accesibles desde Aurora no cambia el hecho de que algunas pueden tener funciones de seguimiento incorporadas. No siempre será posible, pero siempre que puedas, busca una alternativa de F-Droid antes de descargar a través de Aurora.

Para instalar Aurora, simplemente busca 'Aurora Store' en F-Droid.

Aurora también tiene algunos posibles vectores de ataque, ya que las "cuentas anónimas" son realmente creadas y controladas por Aurora. En teoría, podrían servir actualizaciones maliciosas o enviar aplicaciones a tu teléfono, aunque aún tendrías que aceptar la solicitud de instalación en el dispositivo. Aurora también a veces tiene problemas con las aplicaciones que no aparecen debido a errores de región y lectura incorrecta del dispositivo. Esto generalmente se puede solucionar con los siguientes pasos.

**Consejo principal** - A veces, Aurora Store experimentará limitación de velocidad que limita tu capacidad para buscar e instalar aplicaciones. Para solucionar esto, ve a **Configuración** > **Aplicaciones** > **Aurora** > **Abrir por defecto**, luego agrega el dominio `play.google.com`. Ahora, cada vez que navegues a un sitio web de un producto o servicio que tenga el enlace 'Descargar a través de Play Store', al tocarlo se abrirá esa aplicación dentro de Aurora para que la descargues.

![image](assets/6.png)

### Descarga de APK

Las aplicaciones en Android también se pueden descargar e instalar a través de un archivo `.apk`. Esta es una excelente alternativa que no requiere tiendas de aplicaciones de terceros, simplemente descarga el archivo directamente desde el proyecto o el sitio web o repositorio de GitHub del servicio.

La desventaja de este enfoque es que no obtienes actualizaciones automáticas, por lo que deberás estar atento a los canales de comunicación del servicio para conocer las nuevas versiones. Sin embargo, hay un gran proyecto llamado Obtanium que tiene como objetivo solucionar esto. [Obtainium](https://github.com/ImranR98/Obtainium) te permite instalar y actualizar aplicaciones de código abierto directamente desde sus páginas de lanzamiento, y recibir notificaciones cuando se publiquen nuevas versiones.

![image](assets/7.png)

### Aplicaciones web

Para momentos en los que quieras usar un servicio de forma poco frecuente y no quieras descargar una aplicación nativa, simplemente puedes acceder a la versión web. Hoy en día, muchos sitios web también ofrecen soporte para Progressive Web App (PWA). Esto te permite agregar un sitio web específico (por ejemplo, Twitter.com) a la pantalla de inicio de tu teléfono. Luego, cuando toques el icono, se abrirá como una aplicación de pantalla completa sin las distracciones habituales que vienen con la experiencia típica del navegador. Puedes ver un ejemplo de cómo se ve esto a continuación.

Para lograr esto en Vanadium, el navegador nativo de GrapheneOS, simplemente navega al sitio web de tu elección, toca los tres puntos verticales en la esquina superior derecha de la pantalla y luego toca **'Agregar a la pantalla de inicio'**.

La única desventaja de este enfoque es que, debido a que es solo una página web marcada, no recibirás ningún tipo de notificaciones. ¡Aunque algunos podrían ver eso como algo positivo!

![image](assets/8.png)

### Navegadores web

No puedes equivocarte con la opción preempaquetada, Vanadium. La aplicación se comporta de manera idéntica a cualquier otro navegador móvil que haya probado y nunca he tenido problemas de compatibilidad.

Para los momentos en que necesites acceder a sitios nativos de Tor `.onion`, puedes descargar directamente el APK del Navegador Tor desde su [sitio web](https://www.torproject.org/download/#android) o a través de F-Droid.

### VPNs

Para proteger tu actividad en línea de tu proveedor de servicios de internet (ISP) que espía, una aplicación de Red Privada Virtual (VPN) es una buena opción. Una VPN envía tu tráfico de internet a través de un túnel encriptado hacia una dirección IP compartida controlada por el proveedor de servicios de VPN para asegurar que la actividad de tu dispositivo no pueda ser vinculada a ti.

Las siguientes son 3 opciones respetadas que te permiten pagar el servicio con Bitcoin y sin proporcionar ninguna información personal. Las 3 opciones están disponibles a través de F-Droid.

- [Mullvad](https://f-droid.org/packages/net.mullvad.mullvadvpn/)
- [Proton](https://f-droid.org/en/packages/ch.protonvpn.android/)
- [iVPN](https://f-droid.org/en/packages/net.ivpn.client/)

### Mensajería

En los últimos años, las soluciones de mensajería encriptada se han vuelto abundantes. Sin embargo, el problema persiste: puedes tener la mejor y más privada opción instalada en tu teléfono, pero si no tienes contactos que la usen, ¿cuál es el punto?

La mayoría de las personas que no tienen interés en la privacidad probablemente estén usando WhatsApp o iMessage. El primero se puede descargar a través de Aurora Store, pero el segundo no funcionará en GrapheneOS (¡obviamente!).

- [Signal](https://signal.org/) es uno de los mensajeros de extremo a extremo más populares que tiene un sólido historial y un conjunto de funciones completas. Signal requiere un número de teléfono para registrarse, por lo que si planeas chatear con personas a las que preferirías que no conocieran tu número de teléfono, tal vez deberías considerar algunas de las alternativas. Signal debe descargarse a través de Aurora Store.
- [Simplex](https://f-droid.org/en/packages/chat.simplex.app/) es un mensajero de extremo a extremo bastante nuevo. No tiene un ID de usuario, no requiere número de teléfono ni información personal. Las personas te encuentran escaneando tu código QR personal o visitando tu enlace único. Simplex también permite a los usuarios avanzados ejecutar su propio servidor para reducir aún más la dependencia de cualquier entidad centralizada. Simplex no tiene un cliente de escritorio, por lo que puede que no sea adecuado si la capacidad de usar múltiples dispositivos es una prioridad para ti. Simplex para Android está disponible a través de F-Droid.
- [Threema](https://threema.ch/en/faq/libre_installation) ofrece una experiencia similar a Simplex, pero ha estado disponible por más tiempo y, como resultado, se siente un poco más pulido. Threema no es gratuito, una licencia de por vida cuesta $4.99 y se puede comprar con Bitcoin. Threema ofrece un cliente web y aplicaciones de escritorio nativas. La aplicación de Android está disponible a través de F-Droid.
- [Telegram FOSS](https://f-droid.org/en/packages/org.telegram.messenger/) es una bifurcación no oficial de código abierto del aplicación oficial de Telegram para Android. Telegram tiene 'chats secretos' de extremo a extremo, pero la opción predeterminada no es privada. Telegram FOSS se puede descargar desde F-Droid.

![image](assets/9.png)

### Medios

- [Spotube](https://f-droid.org/packages/oss.krtirtho.spotube/) es un cliente de Spotify multiplataforma que no requiere una cuenta Premium. Spotube está disponible a través de F-Droid.
- [ViMusic](https://f-droid.org/en/packages/it.vfsfitvnm.vimusic/) es una aplicación fantástica para transmitir música de YouTube de forma gratuita. ViMusic está disponible en F-Droid.
- [Newpipe](https://f-droid.org/packages/org.schabi.newpipe/) ofrece una experiencia de YouTube sin los molestos anuncios y permisos cuestionables. Con NewPipe puedes suscribirte a canales, escuchar en segundo plano e incluso descargar para ver sin conexión. NewPipe se puede acceder a través de F-Droid.
- [AntennaPod](https://f-droid.org/packages/de.danoeh.antennapod/) es un reproductor de podcasts que te permite suscribirte y gestionar todos tus programas favoritos. AntennaPod está disponible a través de F-Droid.

![image](assets/11.png)

### Mapas

Si deseas asistencia por voz mientras conduces y utilizas una aplicación de mapas en GrapheneOS, deberás instalar [RHVoice](https://rhvoice.org/installation/) y [configurarlo](https://discuss.grapheneos.org/d/2488-organic-maps-app-voice-instructions-are-not-available).

- [Magic Earth](https://www.magicearth.com/) es una alternativa de mapas que admite navegación paso a paso, mapas en 3D y sin conexión. Magic Earth se puede descargar desde Aurora Store.
- [Organic Maps](https://f-droid.org/en/packages/app.organicmaps/) es una alternativa de mapas para viajeros, turistas, excursionistas y ciclistas basada en datos de OpenStreetMap obtenidos de forma colaborativa. Es una bifurcación de código abierto centrada en la privacidad de la aplicación Maps.me (anteriormente conocida como MapsWithMe). Admite el 100% de las funciones sin conexión a Internet y se puede descargar desde F-Droid.
- [OsmAnd](https://f-droid.org/en/packages/net.osmand.plus/) es otra excelente alternativa de mapas que admite todas las funciones mencionadas anteriormente.

![image](assets/13.png)

### Correo electrónico

- [Proton Mail](https://proton.me/mail) ofrece un servicio de correo electrónico privado gratuito que admite E2EE auditado. Proton también ofrece una versión de pago que admite dominios personalizados y [aliasing](https://proton.me/support/creating-aliases). Proton Mail se puede descargar como un APK directo o a través de Aurora.
- [Tutanota](https://tutanota.com/) ofrece las mismas características que Proton Mail, incluidos servicios pagos opcionales, y se puede descargar como un APK directo o a través de F-Droid.
- [K-9 Mail](https://f-droid.org/en/packages/com.fsck.k9/) es un cliente de correo electrónico de código abierto que funciona con prácticamente todos los proveedores de correo electrónico. Admite múltiples cuentas, una bandeja de entrada unificada y el estándar de cifrado OpenPGP.

![image](assets/15.png)

### Productividad

- [Syncthing](https://f-droid.org/packages/com.nutomic.syncthingandroid/) es un programa de sincronización de archivos. Sincroniza archivos entre dos o más dispositivos en tiempo real, protegidos de miradas indiscretas. Tus datos son solo tuyos y mereces elegir dónde se almacenan, si se comparten con terceros y cómo se transmiten por Internet. Syncthing está disponible a través de F-Droid.
- [KDE Connect](https://f-droid.org/packages/org.kde.kdeconnect_tp/) permite que todos tus dispositivos se comuniquen fácilmente entre sí cuando están conectados a tu red doméstica. Envía fácilmente archivos, fotos y datos del portapapeles a través de todos tus dispositivos (¡incluso en iOS!). KDE Connect se puede descargar desde F-Droid.
- [Notesnook](https://f-droid.org/en/packages/com.streetwriters.notesnook/) es una aplicación de notas E2EE para sincronizar tus pensamientos y listas de tareas en todos tus dispositivos. Su plan gratuito debería cubrir la mayoría de los casos de uso personal. Notesnook está disponible en F-Droid.
- [Standard Notes](https://f-droid.org/en/packages/com.standardnotes/) es muy similar a Notesnook, pero requiere un plan de pago para igualar el conjunto de funciones. Standard Notes está disponible a través de F-Droid.
- [Anysoft Keyboard](https://f-droid.org/packages/com.menny.android.anysoftkeyboard/) es una aplicación de teclado que te permite personalizar prácticamente todo lo que puedas imaginar en cuanto a tu experiencia de escritura en el teléfono. Se puede descargar a través de F-Droid.
- [GBoard](https://play.google.com/store/apps/details?id=com.google.android.inputmethod.latin&hl=en&gl=US) es la aplicación de teclado predeterminada de Google. En mi experiencia, ofrece la mejor experiencia de escritura y deslizamiento. Si descargas esta aplicación, asegúrate de desactivar por completo todos los permisos relacionados con la red. Se puede descargar a través de Aurora.

![image](assets/17.png)

### Estilo de vida

- [Geometric Weather](https://f-droid.org/en/packages/wangdaye.com.geometricweather/) es una aplicación de clima de código abierto bellamente diseñada disponible a través de F-Droid. También admite diferentes tamaños de widgets para que puedas ver el clima en la ubicación que elijas directamente desde la pantalla de inicio.
- [Translate You](https://f-droid.org/packages/com.bnyro.translate/) es una aplicación de traducción de código abierto y privacidad que admite más de 200 idiomas. Translate You está disponible a través de F-Droid.
- [Proton Calendar](https://proton.me/calendar/download) es una aplicación de calendario fácil de usar y E2EE que interactúa perfectamente con tus cuentas de correo electrónico de Proton. Proton Calendar se puede descargar como un APK o a través de la tienda Aurora.
- [PassAndroid](https://f-droid.org/en/packages/org.ligi.passandroid/) es una aplicación para mostrar y almacenar tarjetas de embarque, cupones, entradas de cine y tarjetas de membresía, etc. Simplemente descarga el archivo `pkpass` o `espass` relevante y ábrelo con la aplicación. PassAndroid está disponible a través de F-Droid.

![image](assets/19.png)

### Seguridad/Privacidad

- [Bitwarden](https://mobileapp.bitwarden.com/fdroid/) ofrece una solución gratuita y E2EE de gestión de contraseñas multiplataforma para todos tus dispositivos. Su servicio de pago te permite integrar códigos de 2FA en la aplicación. El servidor de Bitwarden se puede alojar de forma independiente y la aplicación de Android está disponible a través de F-Droid.
- [Proton Pass](https://proton.me/pass/download) ofrece un servicio gratuito similar a Bitwarden, pero los clientes de [Proton Unlimited](https://proton.me/pricing) pueden acceder a funciones avanzadas adicionales. Proton Pass está disponible a través de APK o Aurora.
- [FreeOTP](https://f-droid.org/packages/org.fedorahosted.freeotp/) es una aplicación de autenticación de dos factores para sistemas que utilizan protocolos de contraseñas de un solo uso. Los tokens se pueden agregar fácilmente escaneando un código QR. FreeOTP está disponible a través de F-Droid.
- [Aegis](https://f-droid.org/en/packages/com.beemdevelopment.aegis/) es una aplicación gratuita, segura y de código abierto para Android para gestionar tus tokens de verificación de 2 pasos para tus servicios en línea. Aegis está disponible a través de F-Droid.
- [Cryptomator](https://f-droid.org/en/packages/org.cryptomator.lite/) es un servicio de pago multiplataforma que cifra tus datos localmente para que puedas subirlos de forma segura a tu servicio de almacenamiento en la nube favorito. Cryptomator se puede descargar a través de F-Droid.
  ![image](assets/21.png)

### Soluciones en la Nube

- [Proton Drive](https://proton.me/drive/download) es una solución en la nube de pago con cifrado de extremo a extremo para hacer copias de seguridad y almacenar todos tus archivos. En el momento de escribir esto, acaban de anunciar un cliente de escritorio para Windows, pero los usuarios de Mac y Linux deben seguir utilizando la versión web para sincronizar desde sus computadoras (por ahora). El cliente de Android está disponible como APK o a través de Aurora.
- [Skiff](https://skiff.com/download) también ofrece almacenamiento en la nube de pago con cifrado de extremo a extremo y herramientas de colaboración de archivos. Ofrecen un cliente de escritorio para Mac y Windows (además de una aplicación web) y sus clientes de Android deben descargarse desde Aurora.
- [Nextcloud](https://f-droid.org/en/packages/com.nextcloud.client/) ofrece una solución en la nube completa para la colaboración, sincronización entre dispositivos y almacenamiento de archivos. Los usuarios más avanzados pueden optar por alojar su software libre y de código abierto en cualquier hardware que deseen. Los clientes de Android se pueden descargar a través de F-Droid.
- [Cryptpad](https://cryptpad.fr/) ofrece una alternativa gratuita basada en la web y con cifrado de extremo a extremo a Google Docs.

![image](assets/23.png)

## Las Desventajas

Las alternativas de código abierto y preservación de la privacidad a las aplicaciones de conglomerados tecnológicos a las que te has acostumbrado a usar son abundantes, y algunas de ellas suelen ser mejores que las alternativas de código cerrado y llenas de spyware.

Sin embargo, al cambiar a GrapheneOS, hay algunas comodidades que debes renunciar debido a la falta de alternativas. Estas incluyen:

- **Apple CarPlay/Android Auto** - Tendrás que conformarte con la buena y antigua conexión Bluetooth, USB o Auxiliar.
- **Apple/Google Pay** - ¡Prácticamente todos llevan su billetera consigo de todos modos!
- **Aplicaciones bancarias** - No es que estas no funcionen en absoluto. Algunas funcionan perfectamente de hecho. Otras solo funcionan con los Servicios de Google Play habilitados (lee más al respecto a continuación) y otras simplemente no funcionan en absoluto. Lee el informe de tu banco [aquí](https://privsec.dev/posts/android/banking-applications-compatibility-with-grapheneos/) para ver el estado actual. No te preocupes si el tuyo está en la lista de los que no funcionan, recuerda que puedes guardar la URL como una aplicación web en tu pantalla de inicio.
- **Notificaciones Push** - La mayoría de las aplicaciones que te envían actualizaciones cuando no estás usando una aplicación específica lo hacen a través de los Servicios de Google Play. Estos no están instalados de forma predeterminada en GrapheneOS, por lo que si te encuentras sin recibir notificaciones inmediatas cuando tu amigo te envía un correo electrónico, es probablemente por eso. La buena noticia es que algunas de las aplicaciones mencionadas anteriormente han implementado su propia conexión en segundo plano para verificar periódicamente las actualizaciones y luego enviarte una notificación cuando sea necesario.

### Google Play en un Entorno Aislado

> 'GrapheneOS tiene una capa de compatibilidad que proporciona la opción de instalar y utilizar las versiones oficiales de Google Play en el entorno aislado estándar de la aplicación. Google Play no recibe ningún acceso o privilegio especial en GrapheneOS en comparación con eludir el entorno aislado de la aplicación y recibir una gran cantidad de acceso altamente privilegiado''.
> Si descubres que simplemente no puedes vivir sin esas notificaciones push para tu aplicación favorita o que una cierta aplicación "imprescindible" es inútil sin los Servicios de Google Play, GrapheneOS te permite instalar estos servicios en un entorno completamente aislado. Una vez instalados, estos servicios no requieren una cuenta de Google para funcionar y los permisos de cada uno pueden ser controlados de manera estricta.
> Antes de apresurarte a instalarlos el primer día, te insto a ver hasta dónde llegas sin ellos. Probablemente te sorprenderás de cuántas aplicaciones funcionan perfectamente normalmente sin ellos.

Si deseas instalarlos, simplemente toca la aplicación preinstalada "Apps" seguida de "Google Play Services". Considera instalarlos junto con esas aplicaciones menos privadas de las que no puedes prescindir, dentro de un perfil de usuario completamente separado para proporcionar una capa adicional de segregación del resto de tu teléfono.

![image](assets/24.png)

### Perfiles

GrapheneOS te permite tener una experiencia telefónica separada dentro de tu teléfono. Los perfiles adicionales pueden instalar sus propias aplicaciones y servicios y no pueden acceder a ningún archivo o dato de la cuenta del propietario.
Si solo tienes una o dos de esas aplicaciones imprescindibles que requieren Play Services, pero que solo se utilizan muy ocasionalmente, instalarlas junto con Play Services en un perfil separado puede ser una gran idea para fortalecer aún más cualquier implicación mínima de privacidad que quede al tenerlas en ejecución en el perfil del propietario.

Puedes leer más sobre este caso de uso [aquí](https://discuss.grapheneos.org/d/168-ideas-for-user-profiles/2).

Si decides agregar un perfil separado para adaptarse a tu caso de uso, la aplicación [Insular](https://f-droid.org/en/packages/com.oasisfeng.island.fdroid/) puede ser útil para ti. Insular te permite clonar fácilmente cualquiera de tus aplicaciones existentes en el nuevo perfil sin necesidad de pasar por ninguna de las rutas de instalación tradicionales mencionadas anteriormente en esta guía. Insular también te permite "congelar" rápidamente cualquiera de esas aplicaciones para desactivar por completo todos los servicios en segundo plano de esa aplicación.

![image](assets/25.png)

### e-Sims

Si deseas llevar tu privacidad telefónica al siguiente nivel y tener un servicio celular que esté separado de tu identidad en el mundo real, una eSIM podría ser para ti. Una eSIM es una tarjeta SIM virtual que puedes comprar en línea y agregar a tu teléfono mediante un código QR. Empresas que ofrecen este tipo de servicios que se pueden pagar de forma anónima con Bitcoin incluyen [Silent.Link](https://silent.link/) y [Bitrefill](https://www.bitrefill.com/gb/en/esims/).

Las eSIM no deben considerarse como una panacea completa para la privacidad telefónica. Pueden ser una herramienta útil en manos adecuadas, pero por favor investiga los [compromisos](https://grapheneos.org/faq#cellular-tracking) de usar cualquier tipo de servicio celular si tu intención es estar completamente "fuera de la red".

Los Servicios de Google Play en un entorno aislado deben estar instalados para la provisión de eSIM en GrapheneOS.

## Copias de seguridad

Después de configurar tu nuevo teléfono Pixel sin Google, es una buena idea crear una copia de seguridad. Esta copia de seguridad te permitirá restaurar el teléfono a un estado idéntico en caso de que pierdas tu teléfono o te lo roben.

Puedes elegir almacenar el archivo de copia de seguridad en cualquier medio de almacenamiento externo o en una solución de nube autohospedada como Nextcloud, aunque algunos usuarios informan niveles variables de éxito con esta última opción.

Para crear tu primera copia de seguridad:

1. Ve a **Configuración** > **Sistema** > **Copia de seguridad**, luego anota tu código de recuperación de 12 palabras. Este código es necesario para descifrar el archivo de copia de seguridad en una fecha posterior. Si pierdes el código, perderás el acceso a la copia de seguridad de tu teléfono.
2. A continuación, elige la ubicación de almacenamiento. Recomendaría una unidad USB externa o una tarjeta microSD de grado industrial.
3. Elige los datos que deseas respaldar. Si tienes suficiente espacio en tu medio de almacenamiento especificado, te aconsejaría seleccionar todo.
4. Toca los tres puntos en la parte superior derecha y elige **Realizar copia de seguridad ahora**.

![image](assets/26.png)

Recuerda que si estás haciendo copias de seguridad sin conexión en medios de almacenamiento externos, tiene sentido completar este paso regularmente para asegurarte de que no se pierdan las actualizaciones importantes recientes de tu teléfono en caso de que ocurra lo peor.

![video](https://www.youtube.com/embed/eyWmcItzisk)

## Conclusión

En los últimos años, el software de GrapheneOS ha madurado significativamente. Es más estable y compatible que nunca. Combinado con el floreciente ecosistema de aplicaciones de código abierto y preservación de la privacidad, GrapheneOS se convierte en una alternativa realmente viable a Android o iOS de stock, incluso para personas "normales" como tú.

Las violaciones de datos y la vigilancia masiva son tan comunes en el mundo de hoy que apenas hacen titulares. Depende de ti protegerte. Habrá ajustes y sacrificios que hacer en el camino, pero reducir tu exposición a tales infracciones no es tan difícil como crees que será.

Espero que esta guía te ayude en tu camino. Si encontraste útil esta guía y te gustaría apoyar mi trabajo, considera enviar una [donación](/tips).

Si eres un usuario existente de GrapheneOS, o te conviertes en uno como resultado de esta guía, considera [donar](https://grapheneos.org/donate) para apoyar su importante trabajo.

### Obtén más información

GrapheneOS es un agujero de conejo en el que cualquiera podría pasar fácilmente semanas. Hay tanto que puedes aprender y experimentar para adaptar la experiencia a tus necesidades y modelos de amenazas. A continuación, se muestran algunos enlaces donde puedes continuar tu viaje:

- [Guía oficial de uso de GrapheneOS](https://grapheneos.org/usage) - Sitio web oficial
- [Foro de GrapheneOS](https://discuss.grapheneos.org/) - Sitio web oficial
- [Masterclass de configuración de GrapheneOS](https://www.youtube.com/watch?app=desktop&v=GLJyD9MJgIQ) - Video de 'The Privacy Wayfinder'
- [Podcast general de GrapheneOS](https://www.youtube.com/watch?app=desktop&v=UCPX0mFFRNA) - Podcast de 'Watchman Privacy'

Crédito completo a: https://github.com/BitcoinQnA/Bitcoiner.Guide/blob/main/grapheneos.md
