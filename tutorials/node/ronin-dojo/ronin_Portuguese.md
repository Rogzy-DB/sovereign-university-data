---
name: RoninDojo

description: Instalar e usar seu próprio nó Bitcoin RoninDojo.
---

# Instalar e usar seu próprio nó Bitcoin RoninDojo.

Executar e usar seu próprio nó é essencial para realmente participar da rede Bitcoin. Embora executar um nó Bitcoin não traga nenhum benefício financeiro ao usuário, ele permite preservar sua privacidade, agir de forma independente e controlar sua confiança na rede.

Neste artigo, vamos estudar em detalhes o RoninDojo, uma ótima solução para executar seu próprio nó Bitcoin.

### Sumário:

- O que é o RoninDojo?
- Qual hardware escolher?
- Como instalar o RoninDojo?
- Como usar o RoninDojo?
- Conclusão

Se você não está familiarizado com o funcionamento e o papel de um nó Bitcoin, recomendo começar lendo este artigo: O nó Bitcoin - Parte 1/2: Noções técnicas.

![Samourai](assets/1.png)

## O que é o RoninDojo?

Dojo é um servidor de nó Bitcoin completo desenvolvido pela equipe do Samouraï Wallet. Você pode instalá-lo livremente em qualquer máquina.

RoninDojo é um assistente de instalação e uma ferramenta de administração para o Dojo e várias outras ferramentas. O RoninDojo utiliza a implementação original do Dojo e adiciona muitas outras ferramentas, facilitando sua instalação e gerenciamento.

Eles também oferecem um hardware "plug-and-play", o RoninDojo Tanto, com o RoninDojo pré-instalado em uma máquina montada por sua equipe. O Tanto é uma solução paga, interessante para aqueles que não querem se envolver com a configuração.

O código do RoninDojo é de código aberto, então também é possível instalar essa solução em seu próprio hardware. Essa opção é econômica, mas requer um pouco mais de manipulação, é o que faremos neste artigo.

RoninDojo é um Dojo, portanto, permite integrar facilmente o Whirlpool CLI ao seu nó Bitcoin para ter a melhor experiência possível de CoinJoin. Com o Whirlpool CLI, você não só pode deixar seus bitcoins se misturarem 24 horas por dia, 7 dias por semana, sem precisar deixar seu computador pessoal ligado, mas também pode melhorar significativamente sua privacidade.

RoninDojo inclui muitas outras ferramentas que se baseiam em seu Dojo, como por exemplo: o calculador Boltzmann, que permite determinar o grau de privacidade de uma transação, o servidor Electrum para conectar suas diferentes carteiras Bitcoin ao seu nó ou o servidor Mempool para observar suas transações de forma privada.
Par rapport à une autre solution de nœud comme Umbrel, que je vous ai présentée dans cet article, RoninDojo s'inscrit dans une ligne de développement profondément tournée vers les solutions "On Chain" et vers des outils permettant d'optimiser la confidentialité des utilisateurs. RoninDojo ne permet donc pas d'interagir avec le Lightning Network.

Un RoninDojo propose moins d'outils par rapport à un Umbrel, mais les quelques fonctionnalités essentielles pour un Bitcoiner présentes sur Ronin sont incroyablement stables.

Donc si vous n'avez pas besoin de toutes les fonctionnalités d'un serveur Umbrel, et que vous souhaitez exclusivement disposer d'un nœud simple et stable avec quelques outils essentiels comme Whirlpool ou Mempool, alors RoninDojo est sûrement une bonne solution pour vous.

Selon moi, la ligne de développement d'Umbrel est très tournée vers le Lightning Network et vers des outils polyvalents. Cela reste un nœud Bitcoin, mais on cherche à en faire un mini-serveur multi-tâches. À l'inverse, la ligne de développement de RoninDojo se rapproche plus de celle des équipes de Samourai Wallet, et se focalise sur les outils essentiels d'un Bitcoiner lui permettant une pleine indépendance et un gestion optimisée de sa confidentialité sur Bitcoin.

Veuillez noter que la mise en place d'un nœud RoninDojo reste légèrement plus complexe qu'un nœud Umbrel.

Maintenant que nous avons pu dresser le portrait de RoninDojo, voyons ensemble comment mettre en place ce nœud.

## Quel matériel choisir ?

Pour choisir la machine qui héberge et fait tourner RoninDojo, vous disposez de plusieurs options.

Comme expliqué précédemment, le choix le plus simple sera de commander le Tanto, une machine plug-and-play conçue spécialement pour cet usage. Pour commander le votre, c'est par ici : [https://shop.ronindojo.io/product-category/nodes/](https://shop.ronindojo.io/product-category/nodes/).

Etant donné que les équipes de RoninDojo produisent du code open-source, il est également possible d'implémenter RoninDojo sur d'autres machines. Vous pouvez ainsi retrouver les dernières versions de l'assistant d'installation sur cette page : [https://ronindojo.io/en/downloads.html](https://ronindojo.io/en/downloads.html), et les dernières versions du code sur cette page : [https://code.samourai.io/ronindojo/RoninDojo](https://code.samourai.io/ronindojo/RoninDojo)

Personnellement, je l'ai installé sur un Raspberry Pi 4 8GO et tout fonctionne parfaitement.

Attention tout de même, les équipes de RoninDojo nous indique qu'il y a souvent des problèmes à cause du boitier et de l'adaptateur du SSD. Il est donc déconseillé d'utiliser un boitier avec un câble pour le SSD de votre machine. Préférez plutôt utiliser une carte d'extension de stockage spécialement conçue pour votre carte mère comme celle-ci : Carte d'extension de stockage Raspberry Pi 4.

Voici un exemple de mise en place pour faire votre propre nœud RoninDojo :

- Un Raspberry Pi 4.
- Un boitier avec un ventilateur.
- Uma placa de expansão de armazenamento compatível.
- Um cabo de alimentação.
- Um cartão micro SD industrial de 16GB ou mais.
- Um SSD de 1TB ou mais.
- Um cabo ethernet RJ45, categoria 8 recomendada.

## Como instalar o RoninDojo?

### Etapa 1: Preparar o cartão micro SD bootável.

Depois de montar sua máquina, você poderá começar a instalação do seu RoninDojo. Para fazer isso, comece criando um cartão micro SD bootável gravando a imagem de disco adequada nele.

Insira seu cartão micro SD no seu computador pessoal e acesse o site oficial do RoninDojo para baixar a imagem de disco RoninOS: https://ronindojo.io/en/downloads.html.

Baixe a imagem de disco que corresponda ao seu hardware. No meu caso, baixei a imagem "MANJARO-ARM-RONINOS-RPI4-22.03.IMG.XZ":

![Baixar imagem de disco RoninOS](assets/2.png)

Depois de baixar a imagem, verifique sua integridade usando o arquivo correspondente em .SHA256. Descrevo detalhadamente como fazer isso neste artigo: Como verificar a integridade de um software Bitcoin no Windows?

As instruções específicas para verificar a integridade do RoninOS também estão disponíveis nesta página em inglês: https://wiki.ronindojo.io/en/extras/verify.

Para gravar essa imagem no seu cartão micro SD, você pode usar um software como o Balena Etcher, que pode ser baixado aqui: https://www.balena.io/etcher/.

Para fazer isso, selecione a imagem no Etcher e grave-a no cartão micro SD:

![Gravar imagem de disco com o Etcher](assets/3.png)

Depois que a operação for concluída, você pode inserir o cartão micro SD bootável no Raspberry Pi e ligar a máquina.

### Etapa 2: Configurar o RoninOS.

RoninOS é o sistema operacional do seu nó RoninDojo, é uma versão modificada do Manjaro, uma distribuição Linux. Depois de iniciar sua máquina e esperar alguns minutos, você poderá começar a configurá-la.

Para se conectar remotamente, você precisará encontrar o endereço IP da sua máquina RoninDojo. Para fazer isso, você pode, por exemplo, acessar o painel de administração do seu roteador, ou também pode baixar um software como o https://angryip.org/ para escanear sua rede local e encontrar o IP da máquina.

Depois de encontrar o IP, você poderá acessar sua máquina de outro computador conectado à mesma rede local usando SSH.

Em um computador com MacOS ou Linux, basta abrir o terminal. Em um computador com Windows, você pode usar uma ferramenta especializada como o Putty ou o próprio Windows PowerShell.

Depois de abrir o terminal, digite o seguinte comando:

> ssh root@192.168.?.?

Substitua os dois pontos de interrogação pelo IP do seu RoninDojo encontrado anteriormente.

> Dica: Em um Shell, clique com o botão direito para colar um elemento.

Em seguida, você será levado para o painel de configuração do Manjaro. Escolha a disposição correta do seu teclado usando as setas para mudar o alvo na lista suspensa.

![Configuração do teclado Manjaro](assets/4.png)

Escolha um nome de usuário e uma senha para a sua sessão. Use uma senha forte e faça um backup seguro dela. Você pode eventualmente usar uma senha fraca durante a instalação e, em seguida, facilmente alterar essa senha com a opção de "copiar e colar" no RoninUI. Isso permitirá que você use uma senha muito forte sem ter que gastar muito tempo digitando manualmente durante a configuração do Manjaro.

![Configuração do nome de usuário Manjaro](assets/5.png)

Em seguida, você também será solicitado a escolher uma senha root. Para a senha root, insira diretamente uma senha forte. Você não terá a opção de alterá-la posteriormente no RoninUI. Lembre-se também de fazer um backup seguro dessa senha root.

Em seguida, insira sua localidade e fuso horário.

![Configuração do fuso horário Manjaro](assets/6.png)

![Configuração da localidade Manjaro](assets/7.png)

Em seguida, escolha um nome de host.

![Configuração do nome de host Manjaro](assets/8.png)

Por fim, verifique as informações de configuração do Manjaro e confirme.

![Verificação das informações de configuração do ManjaroOS](assets/9.png)

### Etapa 3: Baixar o RoninDojo.

A configuração inicial do RoninOS será feita. Assim que estiver concluída, como na captura de tela acima, a máquina será reiniciada. Aguarde alguns instantes e, em seguida, digite o seguinte comando para se reconectar à sua máquina RoninDojo:

> ssh pseudo@192.168.?.?

Substitua "pseudo" pelo nome de usuário que você escolheu anteriormente e substitua os pontos de interrogação pelo IP do seu RoninDojo.

Em seguida, insira sua senha de usuário.

No terminal, será assim:

![Conexão SSH ao RoninOS](assets/10.png)

Agora você está conectado à sua máquina que possui apenas o RoninOS no momento. Agora você precisa instalar o RoninDojo.

Baixe a versão mais recente do RoninDojo digitando o seguinte comando:

> git clone https://code.samourai.io/ronindojo/RoninDojo

O download será rápido. No terminal, você verá o seguinte:

![Clonando o RoninDojo](assets/11.png)

Aguarde o término do download e, em seguida, instale e acesse a interface do usuário do RoninDojo usando o seguinte comando:

> ~/RoninDojo/ronin

Você será solicitado a inserir sua senha de usuário:

![Verificação da senha do nó Bitcoin](assets/12.png)'

> Esta comando é necessário apenas na primeira vez que você acessa o seu RoninDojo. Depois, para acessar o RoninCLI via SSH, você só precisa digitar o comando [SSH pseudo@192.168.?.?] substituindo "pseudo" pelo seu nome de usuário e colocando o IP do seu nó. Será solicitada a sua senha de usuário.

Em seguida, você verá esta bela animação:

![Animação de inicialização do RoninCLI](assets/13.png)

Então você finalmente chegará à interface de usuário CLI do RoninDojo.

### Etapa 4: Instalar o RoninDojo.

No menu principal, vá para o menu "System" usando as setas do seu teclado. Use a tecla Enter para confirmar sua escolha.

![Navegação do menu RoninCLI para System](assets/14.png)

Em seguida, vá para o menu "System Setup & Install".

![Navegação do menu RoninCLI para instalação do sistema RoninDojo](assets/15.png)

Por fim, marque "System Setup" e "Install RoninDojo" usando a barra de espaço e selecione "Aceitar" para iniciar a instalação.

![Confirmação da instalação do RoninDojo](assets/16.png)

Deixe a instalação prosseguir tranquilamente. No meu caso, levou cerca de 2 horas. Mantenha o seu terminal aberto durante a operação.

Verifique ocasionalmente o seu terminal, você será solicitado a pressionar uma tecla em certos estágios da instalação, como aqui, por exemplo:

![Instalação do RoninDojo em andamento](assets/17.png)

No final da instalação, você verá os diferentes contêineres iniciando:

![Inicialização dos contêineres do nó](assets/18.png)

Em seguida, o seu nó será reiniciado. Conecte-se novamente ao RoninCLI para a próxima etapa.

![Reinicialização do nó Bitcoin](assets/19.png)

### Etapa 5: Baixar a cadeia de prova de trabalho e acessar o RoninUI.

Após a conclusão da instalação, o seu nó começará a baixar a cadeia de prova de trabalho do Bitcoin. Isso é chamado de IBD (Initial Block Download). Isso geralmente leva entre 2 e 14 dias, dependendo da sua conexão com a internet e do seu dispositivo.

Você pode acompanhar o progresso do download da cadeia acessando a interface web do RoninUI.

Para acessá-lo a partir de uma rede local, digite no seu navegador na barra de endereço:

- Ou diretamente o endereço IP da sua máquina (192.168.?.?)

- Ou: ronindojo.local

Lembre-se de desativar sua VPN, se estiver usando uma.

### Possível reviravolta

Se você não conseguir se conectar ao RoninUI pelo seu navegador, verifique o funcionamento correto do aplicativo a partir do seu Terminal conectado ao seu nó via SSH. Conecte-se ao menu principal seguindo as etapas anteriores:

- Digite: SSH pseudo@192.168.?.? substituindo com suas credenciais.

- Insira sua senha de usuário.
  Une vez no menu principal, vá para:
  > RoninUI > Reiniciar

Se a aplicação reiniciar corretamente, o problema está na conexão do seu navegador. Verifique se você não está usando uma VPN e verifique se está conectado à mesma rede que o seu nó.

Se a reinicialização retornar um erro, tente atualizar o sistema operacional e reinstalar o RoninUI. Para atualizar o sistema operacional:

> Sistema > Atualizações de Software > Atualizar Sistema Operacional

Após a atualização e reinicialização concluídas, reconecte-se ao seu nó via SSH e reinstale o RoninUI:

> RoninUI > Reinstalar

Após baixar novamente o RoninUI, tente se conectar ao RoninUI pelo seu navegador.

> Dica: Se você sair do RoninCLI acidentalmente e acabar no terminal Manjaro, basta digitar o comando "ronin" para voltar diretamente ao menu principal do RoninCLI.

### Login na web

Você também pode se conectar à interface web do RoninUI de qualquer rede usando o Tor. Para fazer isso, obtenha o endereço Tor do seu RoninUI no RoninCLI:

> Credenciais > Ronin UI

Obtenha o endereço Tor terminando com .onion e faça login no Ronin UI inserindo esse endereço no seu navegador Tor. Tenha cuidado para não vazar suas credenciais, pois são informações sensíveis.

![Interface web de login do RoninUI](assets/20.png)

Depois de fazer login, será solicitada a sua senha de usuário. É a mesma que você usa para fazer login via SSH.

![Painel de controle da interface web do RoninUI](assets/21.png)

Podemos ver o progresso do IBD. Tenha paciência, você está recuperando todas as transações feitas no Bitcoin desde 3 de janeiro de 2009.

Após baixar toda a cadeia de blocos, o indexador compactará o banco de dados. Essa operação leva cerca de 12 horas. Você também pode acompanhar o progresso em "Indexer" no RoninUI.

Seu nó RoninDojo estará completamente funcional após isso:

![Indexador sincronizado em 100% nó funcional](assets/22.png)

Se você deseja alterar a senha do usuário para uma mais forte, pode fazê-lo agora na guia "Configurações". No RoninDojo, não há camada de segurança adicional, então recomendo que você escolha uma senha realmente forte e cuide bem de sua segurança.

## Como usar o RoninDojo?

Após baixar e compactar a cadeia, você poderá começar a aproveitar os serviços oferecidos pelo seu novo nó RoninDojo. Vamos ver juntos como usá-los.

### Conectar seus softwares de carteira ao electrs.

La première utilité de votre nœud fraîchement installé et synchronisé sera de diffuser vos transactions au réseau Bitcoin. Vous allez donc sûrement vouloir y connecter vos différents logiciels de gestion de portefeuilles.

Vous pouvez faire cela grâce à Electrum Rust Server (electrs). L'application est normalement préinstallée sur votre nœud RoninDojo. Si ce n'est pas le cas, vous pouvez l'installer manuellement depuis l'interface RoninCLI.

Allez simplement dans :

> Applications > Manage Applications > Install Electrum Server

Pour obtenir l'adresse Tor de votre Electrum Server, depuis le menu RoninCLI, allez dans :

> Credentials > Electrs

Vous n'aurez plus qu'à entrer le lien en .onion sur le logiciel de votre portefeuille. Par exemple sur Sparrow Wallet, il suffit d'aller dans l'onglet :

> File > Preferences > Server

En type de serveur, sélectionnez "Private Electrum", puis entrez l'adresse Tor de votre Serveur Electrum dans la case correspondante. Enfin, cliquez sur "Test Connection" pour tester et enregistrer votre connexion.

![Interface de connexion de Sparrow Wallet à un electrs](assets/23.png)

### Connecter ses logiciels de portefeuilles à Samourai Dojo.

Plutôt que d'utiliser Electrs, vous pouvez également utiliser Samourai Dojo pour connecter votre portefeuille logiciel compatible à votre nœud RoninDojo. Par exemple, Samourai Wallet propose cette option.

Pour ce faire, il suffira de scanner le QR code de connexion de votre Dojo. Pour y accéder depuis RoninUI, cliquez sur l'onglet "Dashboard" puis sur le bouton "Manage" dans la case de votre Dojo. Vous pourrez ensuite voir les QR codes de connexion à votre Dojo et à BTC-RPC Explorer. Pour les mettre en clair, cliquez sur "Display values".

![Récupération du QRcode de connexion au Dojo](assets/24.png)

Pour connecter votre portefeuille Samourai Wallet à votre Dojo, vous devrez scanner ce QR code à l'installation de l'application :

![Connexion à Dojo depuis l'application Samourai Wallet](assets/25.png)

### Utiliser son propre Explorer Mempool.

Outil essentiel du Bitcoiner, l'explorer vous permet de vérifier différentes informations sur la chaîne Bitcoin. Avec Mempool, vous pouvez par exemple vérifier en temps réel les frais appliqués par les autres utilisateurs afin d'ajuster au mieux les vôtres. Vous pouvez également vérifier le stade de confirmation d'une de vos transactions, ou encore regarder le solde d'une adresse.

Ces outils d'explorer peuvent vous exposer à des risques de perte de confidentialité et vous obligent à faire confiance à la base de données d'un tiers. Lorsque vous utilisez cet outil en ligne sans passer par votre propre nœud :

- Vous risquez de faire fuiter des informations sur votre portefeuille.

- Vous faites confiance au gestionnaire du site web pour la chaîne de preuve de travail qu'il héberge.
  A fim de evitar esses riscos, você pode usar sua própria instância Mempool em seu nó através da rede Tor. Com essa solução, não apenas você preserva sua privacidade ao usar o serviço, mas também não precisa mais confiar em um provedor, pois consulta seu próprio banco de dados.

Para isso, comece instalando o Mempool Space Visualizer a partir do RoninCLI:

> Aplicativos > Gerenciar Aplicativos > Instalar Mempool Space Visualizer

Depois de instalado, obtenha o link para o seu Mempool. O endereço Tor permitirá que você acesse de qualquer rede. Da mesma forma, obtemos esse link através do RoninCLI:

> Credenciais > Mempool

![Recuperando endereço Tor do Mempool](assets/26.png)

Basta inserir seu endereço Mempool Tor no navegador Tor para desfrutar de sua própria instância Mempool, baseada em seus próprios dados. Sugiro que você adicione esse endereço Tor aos seus favoritos para acessá-lo mais rapidamente. Você também pode criar um atalho na sua área de trabalho.

![Interface Mempool Space](assets/27.png)

Se você ainda não tem o navegador Tor, pode baixá-lo aqui: https://www.torproject.org/download/

Você também pode acessá-lo pelo seu smartphone instalando o Tor Browser e inserindo o mesmo endereço. De qualquer lugar, você poderá verificar o estado da cadeia Bitcoin usando seu próprio nó.

### Usando o Whirlpool CLI.

Seu nó RoninDojo também inclui o WhirlpoolCLI, uma interface de linha de comando remota para automatizar as misturas Whirlpool.

Quando você realiza um CoinJoin com a implementação Whirlpool, o aplicativo que você está usando deve permanecer aberto para executar misturas e remixes. Esse processo pode ser tedioso para o usuário que deseja ter conjuntos anônimos elevados, pois o dispositivo que hospeda o aplicativo com Whirlpool deve permanecer ligado o tempo todo. Em termos concretos, isso significa que se você deseja envolver suas UTXO em remixes 24 horas por dia, 7 dias por semana, precisará deixar seu computador pessoal ou telefone ligado o tempo todo com o aplicativo aberto.

Uma solução para essa restrição é usar o WhirlpoolCLI em uma máquina destinada a ficar ligada o tempo todo, como um nó Bitcoin. Com isso, nossas UTXO podem ser remixadas 24 horas por dia, 7 dias por semana, sem a necessidade de deixar outra máquina além do nosso nó Bitcoin em funcionamento.
'WhirlpoolCLI is used with WhirlpoolGUI, a graphical interface to be installed on a personal computer that allows easy management of Coinjoins. I explain in detail how to set up Whirlpool CLI with your own dojo in this article: https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin#:~:text=dans%20cette%20partie.-,Tutoriel%20%3A%20Whirpool%20CLI%20sur%20Dojo%20et%20Whirlpool%20GUI.,-Si%20vous%20souhaitez
To learn more about Coinjoin in general, I explain everything in this article: https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin

### Using Whirlpool Stat Tool.

After performing CoinJoins with Whirlpool, you may want to know concretely what is the level of privacy of your mixed UTXOs. Whirlpool Stat Tool allows you to do this easily. With this tool, you can calculate the prospective score and the retrospective score of your mixed UTXOs. To learn more about the calculation of these Anon Sets and how they work, I recommend reading this section: https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin#:~:text=perdre%20en%20confidentialit%C3%A9.-,Anon%20Sets.,-Comme%20expliqu%C3%A9%20pr%C3%A9c%C3%A9demment

The tool is pre-installed on your RoninDojo. For now, it is only available from RoninCLI. To launch it from the main menu, go to:

> Samourai Toolkit > Whirlpool Stat Tool

The instructions for use will scroll. Once this is done, press any key to access the command lines:

![Whirlpool Stats Tool software home](assets/28.png)

You will see the terminal displayed:

> wst#/tmp>

To exit this interface and return to the RoninCLI menu, simply type the command:

> quit

To start, we will set the proxy on Tor in order to be able to extract the OXT data with complete confidentiality. Type the command:

> socks5 127.0.0.1:9050

Then download the data from the pool that contains your transaction:

> download 0001
>
> Replace 0001 with the pool denomination code you are interested in.

The denomination codes are as follows on WST:

- Pool 0.5 bitcoins: 05

- Pool 0.05 bitcoins: 005

- Pool 0.01 bitcoins: 001

- Pool 0.001 bitcoins: 0001

![Downloading data from pool 0001 from OXT](assets/29.png)

Once the data is downloaded, load it with the command:

> load 0001
>
> Replace 0001 with the pool denomination code you are interested in.'
> '![Chargement des données de la pool 0001](assets/30.png)
> Deixe o carregamento ser feito, isso pode levar alguns minutos. Após carregar os dados, digite o comando score seguido do seu TXID (identificador de transação) para obter seus Anon Sets:

> score TXID
>
> Substitua TXID pelo identificador da sua transação.

![Impressão dos scores prospectivos e retrospectivos do TXID fornecido](assets/31.png)

O WST então exibe o score retrospectivo (métricas retrospectivas) e o score prospectivo (métricas prospectivas). Além dos scores dos Anon Sets, o WST também fornece a taxa de difusão da sua saída na pool com base no anon set.

Observe que o score prospectivo da sua UTXO é calculado a partir do TXID da sua mistura inicial, e não do seu último mix. Por outro lado, o score retrospectivo de uma UTXO é calculado a partir do TXID do último ciclo.

Mais uma vez, se você não entender esses conceitos de Anon Sets, recomendo que leia esta parte do meu artigo sobre Coinjoin, onde explico tudo em detalhes com diagramas: https://www.pandul.fr/post/comprendre-et-utiliser-le-coinjoin-sur-bitcoin#:~:text=perdre%20en%20confidentialit%C3%A9.-,Anon%20Sets.,-Comme%20expliqu%C3%A9%20pr%C3%A9c%C3%A9demment

### Utilizando a calculadora Boltzmann.

A calculadora Boltzmann é uma ferramenta que permite calcular facilmente várias métricas avançadas em uma transação Bitcoin, incluindo seu nível de entropia. Todos esses dados permitem que você coloque números no nível de confidencialidade de uma transação e detecte possíveis erros. Essa ferramenta está pré-instalada no seu nó RoninDojo.

Para acessá-la no RoninCLI, conecte-se via SSH e vá para o menu:

> Samourai Toolkit > Boltzmann Calculator

Antes de explicar como usá-la no RoninDojo, vou explicar o que essas métricas representam, como são calculadas e para que servem.

Esses indicadores podem ser usados em qualquer transação Bitcoin, mas são particularmente interessantes para estudar a qualidade de uma transação Coinjoin.

1. O primeiro indicador calculado por esse software é o número de combinações possíveis. Ele é indicado no calculador como "nb combinations". Com base nos valores das UTXOs, esse indicador representa o número de mapeamentos possíveis das entradas para as saídas.

> Se você não está familiarizado com o termo "UTXO", recomendo que leia este breve artigo: Mecanismo de uma transação Bitcoin: UTXO, inputs e outputs.'
> Em outras palavras, esse indicador representa o número de interpretações possíveis para uma transação específica. Por exemplo: uma Coinjoin com estrutura Whirlpool 5x5 terá um número de combinações possíveis igual a 1496:
> ![Esquema de uma transação Coinjoin em kycp.org](assets/32.png)

Crédito: https://kycp.org/#/fe5e5abab7ea452f87603f7ebc2fa4e77380eafcc927e1cb51e1a72401ab073d

2. O segundo indicador calculado é a entropia de uma transação ("Entropia"). Dado que o número de combinações possíveis pode ser muito alto para uma transação, pode-se optar por usar a entropia. A entropia representa o logaritmo binário do número de combinações possíveis. Sua fórmula é a seguinte:

- E: entropia da transação.

- C: número de combinações possíveis para a transação.

> E = log2(C)

Em matemática, o logaritmo binário (base 2) é a função inversa da função potência de 2. Em outras palavras, o logaritmo binário de x é a potência à qual o número 2 deve ser elevado para obter o valor x.

Assim:

> E = log2(C)
> C = 2^E

Portanto, esse indicador é expresso em bits. Por exemplo, aqui está o cálculo da entropia de uma transação Coinjoin com estrutura Whirlpool 5x5, com o número de combinações possíveis igual a 1496:

> C = 1496
>
> E = log2(1496)
>
> E = 10.5469 bits

Essa transação Coinjoin possui uma entropia de 10.5469 bits, o que é muito bom.

Quanto maior esse indicador, mais interpretações diferentes da transação existem e, portanto, mais confidencial é a transação.

Vamos considerar outro exemplo. Aqui está uma transação "clássica" que possui uma entrada e duas saídas:

![Esquema de transação bitcoin em oxt.me](assets/34.png)

Crédito: https://oxt.me/graph/transaction/tiid/9815286

Essa transação possui apenas uma única interpretação possível:

> [(inp 0) > (Outp 0 ; Outp 1)]

Portanto, sua entropia será igual a 0:

> C = 1
>
> E = log2(C)
>
> E = 0

3. O terceiro indicador fornecido pelo calculador Boltzmann é a eficiência da Tx chamada "Eficiência da Carteira". Esse indicador simplesmente permite comparar a transação de entrada com a melhor transação possível na mesma configuração.
   Vamos então introduzir o conceito de entropia máxima, que representa a entropia mais alta alcançável para uma estrutura de transação dada. Por exemplo, a estrutura de Coinjoin do tipo Whirlpool 5x5 terá uma entropia máxima igual a 10.5469. O indicador de eficiência compara então essa entropia máxima com a entropia real da transação de entrada. Sua fórmula é a seguinte para:

- ER: Entropia real expressa em bits.

- EM: Entropia máxima com a mesma estrutura expressa em bits.

- Ef: Eficiência expressa em bits.

> Ef = ER - EM
>
> Ef = 10.5469 - 10.5469
>
> Ef = 0 bits

Esse indicador também é expresso em porcentagem, então sua fórmula é a seguinte para:

- CR: Número de combinações possíveis reais.

- CM: Número de combinações possíveis no máximo com a mesma estrutura.

- Ef: Eficiência expressa em porcentagem.

> Ef = CR/CM
>
> Ef = 1496/1496
>
> Ef = 100%

Uma eficiência de 100% significa que essa transação tem a maior privacidade possível em relação à sua estrutura.

4. O quarto indicador calculado é a densidade da entropia ("Entropy Density"). Isso permite relacionar a entropia a cada entrada ou saída. Assim, podemos usar esse indicador para comparar a eficiência entre várias transações de tamanhos diferentes.

Seu cálculo é muito simples, vamos dividir a entropia da transação pelo número de inputs e outputs presentes nela. Por exemplo, para um Coinjoin do tipo Whirlpool 5x5, teremos:

    ED: Densidade da entropia expressa em bits.

    E: Entropia da transação expressa em bits.

    T: número total de inputs e outputs na transação.

T = 5 + 5 = 10
ED = E / T
ED = 10.5469 / 10
ED = 1.054 bits

A quinta informação fornecida pelo calculador Boltzmann é a tabela de probabilidades de links entre as entradas e saídas. Essa tabela simplesmente fornecerá a probabilidade (pontuação de Boltzmann) de uma entrada dada corresponder a uma saída dada.

Se pegarmos nosso exemplo com um Coinjoin Whirlpool, a tabela de probabilidades será:

| Input | Output 0 | Output 1 | Output 2 | Output 3 | Output 4 |
| ----- | -------- | -------- | -------- | -------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0     | 34%      | 34%      | 34%      | 34%      | 34%      |
| 1     | 34%      | 34%      | 34%      | 34%      | 34%      |
| 2     | 34%      | 34%      | 34%      | 34%      | 34%      |
| '     | 3        | 34%      | 34%      | 34%      | 34%      | 34% |     | 4   | 34% | 34% | 34% | 34% | 34% |

Aqui podemos ver que cada input tem a mesma probabilidade de estar relacionado a cada output.

No entanto, se tomarmos o exemplo de uma transação com um input e dois outputs, então teremos:

| Input | Output 0 | Output 1 |
| ----- | -------- | -------- |
| 0     | 100%     | 100%     |

Neste exemplo, podemos ver que a probabilidade de cada output vir do input 0 é de 100%.

Quanto menor essa probabilidade, maior será a confidencialidade.

6. A sexta informação calculada é o número de links determinísticos. Também será fornecida a proporção de links determinísticos. Esse indicador destaca o número de links entre inputs e outputs da transação que têm uma probabilidade de 100%, ou seja, são indiscutíveis.

A proporção indica o número de links determinísticos na transação em relação ao número total de links.

Por exemplo, uma transação Coinjoin Whirlpool não tem nenhum link determinístico entre as entradas e saídas. O indicador será igual a zero e a proporção também será de 0%.

No entanto, para a segunda transação estudada (1 input e 2 outputs), o indicador é igual a 2 e a proporção é igual a 100%.

Portanto, se esse indicador for igual a zero, isso indica uma boa confidencialidade.

Agora que estudamos os indicadores, vamos ver como calculá-los usando este software. No RoninCLI, vá para o menu:

> Samourai Toolkit > Boltzmann Calculator

![Página inicial do software Boltzmann Calculator](assets/35.png)

Depois de iniciar o software, digite o ID da transação que você deseja estudar. Você pode inserir várias transações separadas por vírgula e pressionar Enter:

![Digite um TXID para estudar no Boltzmann Calculator](assets/36.png)

O calculador então retorna todos os indicadores que vimos anteriormente:

![Impressão dos dados do Boltzmann Calculator para este TXID](assets/37.png)

Digite o comando "Quit" para sair do software e voltar ao menu do RoninCLI.

Para saber mais sobre o calculador Boltzmann, recomendo a leitura destes artigos:

- https://medium.com/@laurentmt/introducing-boltzmann-85930984a159

- https://gist.github.com/LaurentMT/e758767ca4038ac40aaf

### Conectar ao Bisq.

Bisq é uma plataforma de troca que permite comprar e vender bitcoins peer-to-peer. Ele é usado com um software de desktop que é executado no Tor e permite trocar bitcoins sem precisar fornecer sua identidade.'
Bisq garante a segurança das trocas peer-to-peer através de um sistema de multi-assinatura 2/2. Você pode usar este software com seu próprio nó RoninDojo para otimizar a privacidade de suas trocas e confiar nos dados do blockchain do seu próprio nó.
Para baixar o software Bisq, visite o site oficial deles: https://bisq.network/

Para começar a usar o software, recomendo que você leia esta página: https://bisq.network/getting-started/

Para obter o link de conexão do seu RoninDojo, você precisará se conectar ao RoninCLI via SSH. Em seguida, vá para o menu:

> Aplicativos > Gerenciar aplicativos

Digite sua senha e marque a caixa com a tecla de espaço:

> [ ] Habilitar conexão Bisq

Confirme sua escolha. Deixe seu nó ser instalado e depois vá buscar o endereço Tor V3 em:

> Credenciais > Bitcoind

Copie o endereço em "Bitcoin Daemon".

Você também pode obter seu endereço Bitcoind Tor V3 pela interface RoninUI clicando em "Gerenciar" na caixa "Bitcoin Core" no "Painel":

![Obter endereço TorV3 Bitcoin Daemon no RoninUI](assets/38.png)

Para conectar seu nó ao Bisq, vá para o menu:

> Configurações > Informações da rede

![Acessar a interface de conexão do nó no software Bisq](assets/39.png)

Clique na bolha "Usar nós Bitcoin Core personalizados". Em seguida, insira seu endereço Bitcoin TorV3 na caixa fornecida, com o ".onion" mas sem o "http://".

![Caixa para inserir o endereço TorV3 do seu nó no software Bisq](assets/40.png)

Reinicie o software Bisq. Seu nó agora está conectado ao seu Bisq.

### Outras funcionalidades.

Seu nó RoninDojo também possui outras funcionalidades básicas. Você tem a opção de escanear informações específicas para garantir que elas sejam consideradas.

Por exemplo, às vezes é possível que sua carteira conectada ao seu RoninDojo não encontre os bitcoins que você possui. O saldo está em 0, mesmo que você tenha certeza de que possui bitcoins nesta carteira. Existem várias possíveis causas a serem consideradas, incluindo um erro nos caminhos de derivação, e uma delas é que seu nó não está observando seus endereços.

Para corrigir isso, você pode verificar se seu nó está rastreando corretamente seu xpub com a ferramenta "xpub tool". Para acessá-la no RoninUI, vá para o menu:

> Manutenção > Ferramenta XPUB

Digite o xpub que está causando o problema e clique em "Verificar" para verificar essa informação.

![Ferramenta XPUB no RoninUI](assets/41.png)

Se seu xpub estiver sendo rastreado corretamente pelo nó, você verá isso:

![Ferramenta XPUB resultado favorável da análise](assets/42.png)
Verifique se todas as transações aparecem corretamente. Verifique também se o tipo de derivação corresponde ao do seu portfólio. Aqui podemos ver que o nó interpreta este xpub como uma derivação BIP44. Se esse tipo de derivação não corresponder ao do seu portfólio, clique no botão "Retype" e selecione BIP44/BIP49/BIP84 de acordo com sua escolha:
![Changer le type de dérivation de la xpub étudiée depuis RoninUI](assets/43.png)

Se o seu xpub não estiver sendo rastreado pelo seu nó, você verá esta tela que o convida a importá-lo:

![Importer une xpub avec outil XPUB Tool sur RoninUI](assets/44.png)

Você também pode usar outras ferramentas de manutenção:

- Transaction Tool: Permite observar os detalhes de uma transação específica.

- Address Tool: Permite verificar se um endereço específico está sendo rastreado pelo seu Dojo.

- Rescan Blocks: Força o seu nó a escanear novamente um intervalo de blocos escolhido.

Você também encontrará na RoninUI a ferramenta "Push Tx". Isso permite que você transmita uma transação assinada para a rede Bitcoin. Ela deve ser inserida no formato hexadecimal:

![Outil de diffusion d'une transaction signée depuis RoninUI](assets/45.png)

## Conclusão.

Vimos como instalar e usar esta maravilhosa ferramenta que é o RoninDojo. É uma excelente escolha para executar seu próprio nó Bitcoin. É uma solução estável que integra e mantém atualizadas todas as ferramentas essenciais para um Bitcoiner.

Se você não tem medo de usar o terminal e não precisa de ferramentas relacionadas à Lightning Network, então o RoninDojo pode ser adequado para você.

Se puder, considere fazer uma doação aos desenvolvedores que produzem esses softwares gratuitos e de código aberto para você: https://donate.ronindojo.io/

Para saber mais sobre o RoninDojo, recomendo que você observe os links em minhas referências externas abaixo.

### Para saber mais:

- Compreender e usar o CoinJoin no Bitcoin.

- Funções de hash - trecho do ebook Bitcoin Démocratisé 1.

- Tudo sobre a Passphrase Bitcoin.

### Referências externas:

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
