---
title: L'infrastructure de  Migale
language: french
traduction: false
authors: 
- Hélène Chiapello, Véronique Martin, Cédric Midoux, Olivier Rué
categories: 
- Documentation
tags:
- migale
level: facile
prerequites:
- commandes-unix
date: 2020-04-15
publishdate: 2020-04-15
draft: false
type: post
thumbnail: migale-orange.png
w3codecolor: true
toc_depth: 4
#comments: true
#bibliography: biblio.bib
#nocite: '@*'
---

Ce post a pour objectif de vous présenter et de vous apprendre à utiliser l’infrastructure mise à disposition par la plateforme <a href="https://migale.inrae.fr>Migale</a> : modalités d’accès (création de compte, connexion au serveur migale), espaces de travail, outils et banques de données, utilisation du cluster de calcul.

***

# Présentation de Migale

<a href="https://migale.inrae.fr">La plateforme de bioinformatique Migale</a> existe depuis 2003 au sein de l’unité MIG, puis <a href="https://maiage.inrae.fr">MaIAGE</a>. Elle a pour missions de fournir une infrastructure de bioinformatique et des services à la communauté des sciences de la vie.

La plateforme Migale fait partie du réseau national des plateformes de bioinformatique et constitue avec huit autres plateformes de la région parisienne (Génoscope CEA, FP4 Pasteur, Bioinfo Curie, URGI, e-Bio Paris-11, RPBS Paris 7, Genatlas Paris 5) le pôle régional APLIBIO (Alliance des PLateformes d’Ile-de-France pour la BIOinformatique). APLIBIO est l’un des six pôles régionaux de l’infrastructure nationale de service en bioinformatique : l’Institut Français de Bioinformatique (IFB). Migale fait également partie de France-Génomique, une infrastructure nationale regroupant des plateformes de séquençage et des plateformes de bioinformatique traitant ce type de données. 
En 2018 la plateforme a été reconnue Infrastructure Scientifique Collective par INRAE. Sous l’impulsion de ses départements scientifiques de tutelle, elle compose, avec les 3 plateformes de bioinformatique GenoToul Bioinfo, URGI et SIGENAE, l’unique  infrastructure de recherche (IR) en bioinformatique, *BioinfOmics*, d’INRAE.

<a href="https://migale.inrae.fr"><img src="../../bandeau_siteweb.png" style="width:50%"></img></a>

## Infrastructure de calcul scientifique

Notre infrastructure informatique comprend un cluster de calcul, des serveurs, des machines virtuelles hébergeant des applications et un système de stockage. Tous sont interconnectés.

<div class="mermaid" style="text-align:center">
graph TD
    I["utilisateur"]
    B["serveur migale"]
    A["cluster de calcul"]
    D["stockage"]
    E["banques"]
    F["outils"]
    I == connexion ==> B
    B == soumission ==> A
    A == restitution ==> B
    B-.-F
    B-.-D
    B-.-E
    A-.-D
    A-.-E
    A-.-F
</div>
<div style="text-align:center"><i>Figure 1 : Organisation simplifiée de l'infrastructure</i></div>

<br>
Le point d'entrée est le serveur migale. Pour s'y connecter, il faut au préalable obtenir un compte.

## Obtenir un compte

Un compte sur la plateforme donne un moyen d'accès à cette infrastructure.

<div class="alert note">
Pour tous les exemples à suivre, l'utilisateur sera <i><em>stage01</em></i>, du groupe <i><em>maiage</em></i>.
</div>

L'obtention d'un compte est possible pour toute personne travaillant sur des données des sciences de la vie. Le formulaire est accessible sur le site de la plateforme : [https://migale.inrae.fr/ask-account](https://migale.inrae.fr/ask-account). Le compte est ouvert le temps du contrat des non permanents (renouvelable sur demande) et illimité pour les permanents.

<img src="../../ask-account.png" style="width:50%"></img>

<div class="alert comment">L'adresse mail demandée est obligatoire. Elle sera ajoutée à la liste de diffusion (user-migale@groupes.renater.fr) regroupant tous les utilisateurs. Cela permet à la fois une diffusion d’informations concernant les interruptions de service, les nouveaux outils disponibles, les changements importants... Pensez à nous avertir si vous en changez !
</div>


# Connexion au serveur migale

Le serveur migale est le point d'accès à notre infrastructure ; c'est un serveur qui utilise l'environnement Unix. Son accès peut se faire de façon différente suivant le système d'exploitation de l'utilisateur (Unix, MacOSX ou Windows).

## <i class="fa fa-linux" aria-hidden="true">&nbsp;</i>Unix ou <i class="fa fa-apple" aria-hidden="true">&nbsp;</i>MacOS 

Sous Unix ou MacOS, l’environnement Unix du serveur migale est accessible via le terminal, qui peut être ouvert avec Ctrl + Alt + T (Unix) ou Menu « Shell » , puis sous-menu "Nouvelle fenêtre basic » (MacOS).

<div class="example">
<p class="title">Se connecter au serveur migale</p>
<pre class="shell"><code class="hljs lua">
local:~$ ssh -X stage01@migale.jouy.inrae.fr
Password:
</code>
</pre>

Le mot de passe, fourni au moment de la demande de compte, est requis.
<div class="alert comment">Le mot de passe entré ne s'affiche pas pour des raisons de sécurité. Soyez bien concentrés lors de la saisie.
</div>

S’affiche alors à l’écran un message d’accueil ainsi que des instructions génériques et actualités.

<pre class="shell"><code class="hljs lua">
local:~$ ssh -X stage01@migale.jouy.inrae.fr
Password:
Last login: Mon Feb 24 11:25:48 2020 from 138.102.22.243
  __  __ _           _     
 |  \/  (_)__ _ __ _| |___ 
 | |\/| | / _` / _` | / -_)
 |_|  |_|_\__, \__,_|_\___|
          |___/           
-----------------------
Bienvenue sur le serveur frontal de la  plateforme Migale,
Vous trouverez la liste des outils disponibles en ligne de commande sur le site de la plateforme :
https://migale.inrae.fr/tools
Merci d utiliser le cluster pour vos calculs. 
Dans tous les cas, ne pas lancer de calcul long (supérieur à 1h) ou utilisant plus de deux processeurs sur ce serveur.
Pour toute question : help-migale@inrae.fr
-----------------------
Welcome to the Migale facility front end server,
You will find the list of command line tools available on our website:
https://migale.inrae.fr/tools
Please use the cluster for your calculations.
In any case, do not run a long jobs (more than 1 hour) or using more than two processors on this server.
For any questions: help-migale@inrae.fr
-----------------------
[stage01@migale ~]$ 
</code>
</pre>
</div>


<details>
<summary>Démonstration en vidéo</summary>
<br>
<video width="80%" controls>
  <source src="../../unix-connection.webm" type="video/webm">
</video>
</details>

## <i class="fa fa-windows">&nbsp;</i> Windows

MobaXterm propose une application logicielle permettant d'utiliser sous Windows les commandes Unix/Linux. Ce logiciel est gratuit et très simple d'utilisation. Pour se connecter, il faut spécifier l'adresse de l'hôte distant (remote host), en l'occurrence `migale.jouy.inrae.fr`, le nom d'utilisateur (username), et enfin le mot de passe.

<details>
<summary>Démonstration en vidéo</summary>
<br>
<video width="80%" controls>
  <source src="../../mobaxterm.webm" type="video/webm">
</video>
</details>

## Changer le mot de passe

Le mot de passe fourni au moment de la création du compte est donné par l'administrateur système. Il faut impérativement le changer via ce site web : <a href="https://migale.jouy.inrae.fr/ssp/">https://migale.jouy.inrae.fr/ssp/</a>.

### Clé SSH

Pour ne pas avoir à fournir le mot de passe à chaque connexion, il est possible de créer une clé ssh. Cela permet d'éviter les oublis et évite la perte de temps due aux fautes de frappe du mot de passe. L'authentification se fait par clé, de façon tout aussi sécurisée.


<div class="example">
<p class="title">Créer une clé ssh</p>

<pre class="shell"><code class="hljs lua">
# Création d’une clé (publique et privée)
local:~$ ssh-keygen -t rsa 

# Envoi de la clé publique sur le serveur migale
local:~$ ssh-copy-id -i ~/.ssh/id_rsa.pub stage01@migale.jouy.inrae.fr 

# Connexion sans mot de passe
local:~$ ssh -X migale.jouy.inrae.fr
Last login: Wed Apr 22 10:25:41 2020 from 77.204.31.85
  __  __ _           _     
 |  \/  (_)__ _ __ _| |___ 
 | |\/| | / _` / _` | / -_)
 |_|  |_|_\__, \__,_|_\___|
          |___/           
-----------------------
Bienvenue sur le serveur frontal de la  plateforme Migale,
Vous trouverez la liste des outils disponibles en ligne de commande sur le site de la plateforme :
https://migale.inrae.fr/tools
Merci d'utiliser exclusivement le cluster pour vos calculs. 
Dans tous les cas, ne pas lancer de calculs longs ou utilisant plus d'un thread sur ce serveur. 
Pour toute question : help-migale@inrae.fr
-----------------------
Welcome to the Migale facility front end server,
You will find the list of command line tools available on our website:
https://migale.inrae.fr/tools
Please use the cluster for your calculations.
In any case, do not run  long jobs or using more than one thread on this server.
For any questions: help-migale@inrae.fr
-----------------------
[stage01@migale ~]$ 

</code></pre>
</div>

# Les espaces de travail

La figure 2 représente l'organisation des comptes utilisateurs. Un répertoire `/projet` regroupe plusieurs répertoires représentant des groupes d'utilisateurs répartis selon leur unité d'affectation pour les agents INRAE ou un répertoire `extern` pour les autres. Dans chacun de ces répertoires se trouvent un répertoire `work` et un répertoire `save`. L'utilisateur `stage01` n'a naturellement accès qu'aux répertoires qui le concernent (en orange sur la figure) ; pour rappel il fait partie du groupe `maiage`. Lors de la connexion, l'utilisateur est dirigé automatiquement dans le `home directory` (entouré en violet sur la figure), correspondant au répertoire `save`.

<div class="mermaid" style="text-align:center">
graph TD
    B["/projet"]
    B-->D["/projet/micalis"]
    B:::someclass-->C["/projet/maiage"]
    B-->E["/projet/..."]
    C:::someclass-->F["/projet/maiage/save"]
    C:::someclass-->G["/projet/maiage/work"]
    F:::someclass-->H["/projet/maiage/save/stage01"]
    F-->I["/projet/maiage/save/..."]
    G:::someclass-->J["/projet/maiage/work/stage01"]
    G-->K["/projet/maiage/work/..."]
    J:::someclass
    F:::someclass
    style H fill:#f96,stroke:#f0,stroke-width:8px
    classDef someclass fill:#f96;
    
</div>
<div style="text-align:center"><i>Figure 2 : Organisation des espaces utilisateurs</i></div>

## Save vs Work

Le répertoire `save` est un espace dédié aux fichiers de configuration du compte (voir `.shellrc` dans le tutoriel <a href="">unix</a>) et aux résultats qui doivent être conservés. Cet espace est doté d'un système de snapshots [à compléter].

Le répertoire `work` est un espace dédié aux fichiers temporaires, qui n'ont pas vocation à être conservés sur une longue période. C'est un espace de travail au quotidien.

## Volumétrie

Les espaces `work` et `save` ont des volumétries distinctes. Actuellement, les quotas sont partagés entre les membres d'un même groupe.

Pour connaître la volumétrie restante dans un répertoire, il faut utiliser la commande `df -h`.

<div class="example">
<p class="title">Connaître l'espace occupé et restant de l'espace /projet/maiage/work</p>
<pre class="shell"><code class="hljs lua">
[stage01@migale ~]$ df -h /projet/maiage/work/
Sys. de fichiers          Taille Utilisé Dispo Uti% Monté sur
nasproj2:/vs2_maiage_work    17T     15T  2,0T  88% /projet/maiage/work
</code></pre>

Dans cet exemple, 88% du répertoire /projet/maiage/work est occupé. Il reste 2,0 To disponibles. En cas d'espace proche de la saturation, un mail est envoyé aux utilisateurs concernés pour libérer de l'espace dans la mesure du possible.

</div>

## Espaces projets

Certains espaces sont dédiés à un projet. Par exemple, l'espace projet _redlosses_ est lié au groupe unix `redlosses`. Chaque membre du groupe `redlosses` peut donc écrire dans les répertoires `work` et `save` associés (Figure 3).

<div class="mermaid" style="text-align:center">
graph TD
    B["/projet"]
    B-->D["/projet/proteore"]
    B:::someclass-->C["/projet/redlosses"]
    B-->E["/projet/..."]
    C:::someclass-->F["/projet/redlosses/save"]
    C:::someclass-->G["/projet/redlosses/work"]
    F:::someclass
    G:::someclass
    classDef someclass fill:#f96;
    
</div>
<div style="text-align:center"><i>Figure 3 : Organisation des espaces projets</i></div>



<pre class="shell"><code>
[orue@migale ~]$ ls -ltrah /projet/redlosses/
total 12K
drwxr-xr-x   4 root root        30 21 avril  2017 .
drwxrwsr-x  15 root redlosses 4,0K 29 mai    2019 work
drwxrwsr-x  15 root redlosses 4,0K 29 mai    2019 save
drwxr-xr-x 117 root root      4,0K  2 avril 16:11 ..
</code></pre>



# Outils

De nombreux outils sont accessibles en ligne de commande. Vous pouvez retrouver la liste complète des outils ici : <a href="https://migale.inrae.fr/tools">https://migale.inrae.fr/tools</a>.

<img src="../../conda.png" style="width:8%; float: left;margin-right: 10px;"></img> 
<br/>
La majorité des outils est installée sous conda. Conda est un gestionnaire de paquets. Il est conçu pour gérer des paquets et dépendances de n'importe quel programme dans n'importe quel langage. Concrètement, les dépendances d'un outil spécifique sont embarquées dans l'environnement conda de l'outil. Il n'a donc pas besoin d'aller les chercher ailleurs. Cela évite des conflits entre dépendances. De plus, un outil installé via conda a sa propre version. Il est plus facile de gérer les versions des outils ainsi.

<img src="../../bioconda.png" style="width:11%; float: left;margin-right: 10px;"></img>
<br/>
La majorité des outils bioinformatiques sont disponibles sur le dépôt Bioconda.


<div class="example">
<p class="title">Lancer la commande blastn de l'outil ncbi-blast+</p>

<pre class="shell"><code>

# Rechercher le nom de l environnement blast si inconnu
[stage01@migale ~]$ conda info --envs |grep blast 
blast-2.9.0

# Ensuite, activer l environnement conda en question
[stage01@migale ~]$ conda activate blast-2.9.0

# Les exécutables sont accessibles
(blast-2.9.0) [stage01@migale ~]$ blastn -version
blastn: 2.9.0+
 Package: blast 2.9.0, build Sep 28 2019 00:38:34

# Lancer la commande
(blast-2.9.0) [stage01@migale ~]$ blastn -db subject.fasta -query query.fasta -out out.blast

# Désactiver l environnement conda
(blast-2.9.0) [stage01@migale ~]$ conda deactivate
[stage01@migale ~]$
</code></pre>

Le nom de l'environnement chargé, ici blast-2.9.0, est indiqué entre parenthèses avant le prompt.

</div>



<div class="alert warning">
Aucun outil ne doit être lancé sur le serveur migale ! Lisez bien la section Cluster de calcul
</div>


# Banques de données


De nombreuses banques de données biologiques publiques sont accessibles sous différents formats (FASTA, genbank, hmm...). Elles sont stockées et accessibles à tous les utilisateurs. Leur mise à jour est effectuée et gérée avec le logiciel BioMAJ, ou manuellement.

Nous utilisons BioMAJ pour gérer la plupart des banques de données. BioMAJ (BIOlogie Mise A Jour) est un moteur de workflow dédié à la synchronisation et au traitement des données.

Elles sont accessibles dans un espace dédié nommé `/db`. La dernière version est localisée dans le répertoire `current` de la banque. Ensuite différents indexes sont accessibles (blast, diamond, hmm...)


<div class="example">
<p class="title">Trouver les indexs blast pour UniProt</p>

<pre class="shell"><code>
[stage01@migale ~]$ ls /db/uniprot/current/
blast  blast.uniprot  diamond  fasta  fasta.uniprot  flat  test.log
[stage01@migale ~]$ ls /db/uniprot/current/blast/
uniprot.00.phr  uniprot.04.psq  uniprot.09.pin  uniprot.14.phr  uniprot.18.psq  uniprot.23.pin  uniprot.28.phr
uniprot.00.pin  uniprot.05.phr  uniprot.09.psq  uniprot.14.pin  uniprot.19.phr  uniprot.23.psq  uniprot.28.pin
uniprot.00.psq  uniprot.05.pin  uniprot.10.phr  uniprot.14.psq  uniprot.19.pin  uniprot.24.phr  uniprot.28.psq
uniprot.01.phr  uniprot.05.psq  uniprot.10.pin  uniprot.15.phr  uniprot.19.psq  uniprot.24.pin  uniprot.29.phr
uniprot.01.pin  uniprot.06.phr  uniprot.10.psq  uniprot.15.pin  uniprot.20.phr  uniprot.24.psq  uniprot.29.pin
uniprot.01.psq  uniprot.06.pin  uniprot.11.phr  uniprot.15.psq  uniprot.20.pin  uniprot.25.phr  uniprot.29.psq
uniprot.02.phr  uniprot.06.psq  uniprot.11.pin  uniprot.16.phr  uniprot.20.psq  uniprot.25.pin  uniprot.30.phr
uniprot.02.pin  uniprot.07.phr  uniprot.11.psq  uniprot.16.pin  uniprot.21.phr  uniprot.25.psq  uniprot.30.pin
uniprot.02.psq  uniprot.07.pin  uniprot.12.phr  uniprot.16.psq  uniprot.21.pin  uniprot.26.phr  uniprot.30.psq
uniprot.03.phr  uniprot.07.psq  uniprot.12.pin  uniprot.17.phr  uniprot.21.psq  uniprot.26.pin  uniprot.pal
uniprot.03.pin  uniprot.08.phr  uniprot.12.psq  uniprot.17.pin  uniprot.22.phr  uniprot.26.psq
uniprot.03.psq  uniprot.08.pin  uniprot.13.phr  uniprot.17.psq  uniprot.22.pin  uniprot.27.phr
uniprot.04.phr  uniprot.08.psq  uniprot.13.pin  uniprot.18.phr  uniprot.22.psq  uniprot.27.pin
uniprot.04.pin  uniprot.09.phr  uniprot.13.psq  uniprot.18.pin  uniprot.23.phr  uniprot.27.psq
</code></pre>

</div>

La liste complète des banques disponibles est accessible ici : <a href="https://migale.inrae.fr/databanks">https://migale.inrae.fr/databanks</a>

# Cluster de calcul

Un cluster est simplement un regroupement d’ordinateurs administrés et organisés ensemble. On appelle ces ordinateurs des *noeuds de calcul* (node). Chaque noeud se caractérise par son nombre de processeurs et sa capacité mémoire. Ce regroupement des noeuds rend possible une gestion globale des ressources de calcul et permet de dépasser les limitations d’un ordinateur individuel. Toutes les informations actualisées sont disponibles sur notre site web : <a href="https://migale.inrae.fr/cluster">https://migale.inrae.fr/cluster</a>.

Les ressources sont accessibles via le serveur migale. Un logiciel est là pour interagir avec les différents noeuds et gérer la répartition des calculs sur les noeuds : il s’agit d’un gestionnaire de jobs (ou Job Scheduler) ; un job représentant un process (une commande). Les jobs sont soumis au gestionnaire, qui les organisera en file d’attente et les distribuera entre les noeuds suivant les ressources souhaitées et disponibles. Le gestionnaire utilisé sur la plateforme Migale est *SGE* (Sun Grid Engine).


## Vocabulaire

### Le processeur

Un noeud d’un cluster contient généralement plusieurs processeurs (CPU) sur lesquels sont exécutées les instructions des programmes informatiques. Dans des conditions classiques d’utilisation, un job est exécuté sur un CPU. Certains programmes sont conçus de manière à pouvoir s’exécuter sur plusieurs CPU simultanément : c’est la parallélisation. Chaque sous-partie parallélisable s’appelle un thread, on parle donc de multithreading. A noter qu’il est possible de paralléliser un calcul uniquement si le programme utilisé le prévoit et exclusivement au sein des CPU d’un même noeud de calcul.

### La mémoire

La mémoire vive, ou random access memory (RAM) est l’espace spécifique consacré aux informations provisoires lors de l’exécution d’un calcul. Les processeurs peuvent y stocker, écrire et lire rapidement des informations binaires. C’est un paramètre très important lors du lancement d’un job sur un cluster. Il est recommandé de lire les recommandations décrites dans la documention du logiciel utilisé pour régler ce paramètre car la valeur par défaut définie par le gestionnaire de jobs n’est pas toujours pertinente.

### Définitions

| Terme | Explication |
|-------|-----|
| noeud | Il s'agit d'un noeud de calcul, donc d'une machine physique. Exemple : `n34` |
| queue | Chaque noeud est associé à une queue et les différentes queues possèdent des caractéristiques propres. Par exemple la file `short.q` autorise les jobs d'une durée maximale de 12 heures |
| job | Process lancé sur le cluster de calcul. Peut être une succession de commandes |

Les noeuds de calcul ont des caractéristiques différentes :

* mémoire
* CPUs

et les queues également :

* durée maximale du job
* accès à certains groupes ou utilisateurs

Les informations à jour sont disponibles sur notre site web : <a href="https://migale.inrae.fr/cluster">https://migale.inrae.fr/cluster</a>.


<div class="example">
La figure suivante représente un cluster de calcul composé de trois noeuds n1, n2 et n3. n1 et n2 ont 4 CPUs et n3 6 CPUs. Trois utilisateurs ont soumis un job. La couleur des CPUs correspond à la couleur des utilisateurs. Par exemple, l'utilisateur a réservé 3 CPUs sur le noeud n1. Les CPUs en vert sont les CPUs qui sont disponibles.

<img src="../../cluster_1.svg" alt="Situation de base">

<p class="title">Cas 1 : L'utilisateur rouge veut lancer un job avec 2 CPUs</p>

<img src="../../cluster_2.svg" alt="Cas 1">

<details>
<summary>Solution</summary>
2 CPUs sont disponibles sur le noeud n2. Le job sera soumis sans attendre.
<img src="../../cluster_3.svg" alt="Cas 1 réponse">
</details>

<p class="title">Cas 2 : L'utilisateur rouge veut lancer un job avec 3 CPUs</p>

<img src="../../cluster_4.svg" alt="Cas 2">

<details>
<summary>Solution</summary>
3 CPUs sont disponibles sur l'ensemble du cluster, mais pas sur le même noeud. Le job sera en attente le temps qu'au moins 1 CPU se libère sur le noeud n2 ou que 2 CPUs se libèrent sur les noeuds n1 ou n3. [expliquer que ce n'est pas possible d'utiliser des CPUs sur des noeuds différents]

<img src="../../cluster_5.svg" alt="Cas 2 réponse">
</details>

</div>


## Soumettre un job

La commande `qsub` permet de soumettre un job sur le cluster, c'est-à-dire déporter les process sur un noeud de calcul. Chaque job se voit assigné un numéro unique. Par défaut, chaque job utilise 1 CPU. Pour utiliser plus de CPUs, il faut utiliser l'option `-pe thread`.

<div class="alert warning">Il est primordial de réserver le bon nombre de CPUs. Si trop de ressources sont réservées, elles ne servent à rien. Si le job utilise plus de ressources que celles réservées, le noeud se retrouve en surcharge. Les conséquences sont soit un ralentissement du job en question et des autres jobs sur le même noeud, soit le plantage du noeud.</div>

Voici les options les plus couramment utilisées :

| Option | Arguments | Exemple | Signification |
|--------|-----------|---------|---------------|
| `-cwd` | / | / | exécuter dans le répertoire courant |
| `-V` | /  | / | transmettre les variables d'environnement de migale au noeud |
| `-N` | `string` | -N myblast | Nom du job |
|	`-b y` | `string` | -b y "ls -l" | Commande(s) à exécuter, entre double quotes |
|	`-q` | `string` | -q short.q | Queue |
|	`-pe thread` | `int` | -pe thread 4 | Nombre de CPUs (threads) dont le job va avoir besoin au maximum |
|	`-l hostname=` | `string` | -l hostname=n68 | Identifiant d'un noeud de la queue choisie |
|	`-o` | `string` | -o myblast.out | Fichier dans lequel sera écrite la sortie standard |
|	`-e` | `string` | -e myblast.err | Fichier dans lequel sera écrite la sortie d'erreur |
|	`-m` | `char` [bea] | -m ea | Envoyer un mail lorsque le job se termine ou est interrompu |
|	`-M` | `string` | -M stage01\@inrae.fr | Adresse mail à laquelle envoyer le mail |

Sans l'option `cwd`, le job est soumis dans le *home directory* de l'utilisateur.

### Soumettre une ligne de commande

L'option `-b y` permet d'écrire la ligne de commande à soumettre directement dans l'instruction de soumission.

<div class="example">
<p class="title">Lancer la commande blast sur le cluster, en utilisant 4 CPUs</p>

<pre class="shell"><code>
[stage01@migale ~]$ qsub -cwd -V -N myblast -pe thread 4 -b y "conda activate blast-2.9.0 && blastn -db subject.fasta -query query.fasta -out out.blast -num_thread 4 && conda deactivate"
Your job 1995190 ("myblast") has been submitted
</code></pre>

Il ne faut surtout pas oublier de charger l'environnement conda de l'outil, et de le désactiver. La syntaxe `&&` permet d'enchaîner les commandes.

</div>

### Soumettre un script

Si vos lignes de commandes à soumettre sont écrites dans un script, il suffit de spécifier le PATH vers le script en dernier argument de la commande `qsub`.

<div class="example">
<p class="title">Soumettre la commande blast écrite dans un script sur le cluster</p>

<pre class="shell"><code>
[stage01@migale ~]$ head myblast.sh
conda activate blast-2.9.0
blastn -db subject.fasta -query query.fasta -out out.blast -num_thread 4
conda deactivate

</code></pre>

Ensuite il faut soumettre ce script avec la commande `qsub`.

<pre class="shell"><code>
[stage01@migale ~]$ qsub -cwd -V -N myblast -pe thread 4 myblast.sh"
Your job 1995190 ("myblast") has been submitted
</code></pre>


<p class="title">Écrire les options de la commande `qsub` dans le script shell</p>

Il est possible de spécifier des options de la commande `qsub` dans le script

<pre class="bash"><code>
#!/bin/bash

### Les commentaires qui commencent par ‘#$’ sont interprétés par SGE comme des options en ligne ###
### ce script est un exemple, il est nécessaire de le modifier pour l'adapter à vos besoins ###

# Shell à utiliser pour l'exécution du job
#$ -S /bin/shell

# Nom du job
#$ -N BLAST_test

# Export de toutes les variables d'environnement
#$ -V

# Utilisateur à avertir
#$ -M <prenom.nom>@inrae.fr

# Avertir au début (b)egin, à la fin (e)nd, à l’élimination (a)bort et à la suspension (s)uspend d’un job
#$ -m bea

# Sortie standard
#$ -o /projet/groupe/save/user/tmp/sge_blast.out

# Sortie d’erreur 
#$ -e /projet/group/save/user/tmp/sge_blast.err

# Lance la commande depuis le répertoire où est lancé le script
#$ -cwd

# Utiliser 4 CPUs
#$ -pe thread 4

# Exemple pour l'utilisation de blast :

DATABANK="subject.fasta"
QUERY="query.fasta"
OUTPUT="out.blast"

conda activate blast-2.9.0
blastn -db $DATABANK -query $QUERY -out $OUTPUT -num_thread 4
conda deactivate

</code></pre>

<pre class="shell"><code>
[stage01@migale ~]$ qsub myblast.sh
Your job 1995190 ("myblast") has been submitted
</code></pre>

</div>

## Soumettre un job-array

Ce type de soumission est particulièrement intéressant dans le cadre de la bioinformatique où plusieurs traitements doivent être effectués indépendamment sur plusieurs échantillons.
La commande `qarray`, qui est en fait un script qui utilise l'option `-t` de `qsub` permet de simplifier pour l'utilisateur cette syntaxe un peu compliquée. Les options de `qsub` peuvent être utilisées.

<div class="example">
<p class="title">Lancer trois blasts simultanément</p>

<pre class="shell"><code>
[stage01@migale ~]$ head myblasts.sh
conda activate blast-2.9.0 && blastn -db subject.fasta -query query1.fasta -out out1.blast -num_thread 4 && conda deactivate
conda activate blast-2.9.0 && blastn -db subject.fasta -query query2.fasta -out out2.blast -num_thread 4 && conda deactivate
conda activate blast-2.9.0 && blastn -db subject.fasta -query query3.fasta -out out3.blast -num_thread 4 && conda deactivate
Your job 1995190 ("myblast") has been submitted
</code></pre>

En lançant ce script avec la commande `qsub`, les trois commandes seraient exécutées de façon séquentielle. Pour les lancer en parallèle sur le cluster, il faut utiliser `qarray` :

<pre class="shell"><code>
[stage01@migale ~]$ qarray -cwd -V -N myblasts -pe thread 4 myblasts.sh
Your job-array 2429606.1-3:1 ("myblasts") has been submitted
</code></pre>

La commande `qstat` renvoie des informations particulières pour les job-arrays.

* Quand les jobs sont en attente :

<pre class="shell"><code>
[stage01@migale ~]$ qstat
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
2429609 0.00000 myblasts   stage01         qw    04/22/2020 18:03:42                                    4 1-3:1
</code></pre>

* Quand les jobs sont lancés :

<pre class="shell"><code>
[stage01@migale ~]$ qstat
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
2429609 0.52079 myblasts   stage01         r     04/22/2020 18:03:53 short.q@n64                        4 1
2429609 0.52079 myblasts   stage01         r     04/22/2020 18:03:53 short.q@n95                        4 2
2429609 0.52079 myblasts   stage01         r     04/22/2020 18:03:53 short.q@n33                        4 3
</code></pre>

Les job-arrays ont donc le même identifiant (2429609) mais se distinguent par leur ja-task-ID (job-array task identifier).

</div>

## Monitorer un job

### Visualiser les jobs

La commande `qstat` donne de nombreuses informations sur les jobs soumis :

| Colonne | Signification |
|---------|---------------|
| job-ID | l'identifiant du job |
| prior | la valeur de priorité |
| name | le nom du job |
| user | l'utilisateur qui a soumis le job |
| state | l'état du job. Peut être `qw` (en attente), `r` (en cours d'exécution), `Eqw` (en erreur) |
| submit/start | date de soumission |
| at | heure de soumission |
| queue | queue d'appartenance du noeud sur lequel le job est exécuté |
| slots | nombre de CPUs demandés |
| ja-task-ID | ID de la tâche du job-array |

<div class="example">
<p class="title">Visualiser les jobs soumis sur le cluster</p>
<pre class="shell"><code>
[stage01@migale ~]$ qstat
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
1995192 0.50500 myblast    stage01         r     10/04/2019 17:11:59 short.q@n35                        1        
</code></pre>

Pour visualiser les jobs des autres utilisateurs, il faut utiliser l'option `-u` (`-u *`) pour voir tous les jobs soumis).
</div>

Une fois que le job est terminé, il n'est plus listé par la commande `qstat`. Pour avoir des informations sur un job terminé, il faut connaître son numéro et utiliser la commande `qacct`.

<div class="example">
<p class="title">Retrouver les informations du job 1995192</p>
<pre class="shell"><code class="">
qacct -j 1995192
==============================================================
qname        maiage.q            
hostname     n68                 
group        mig                 
owner        banko               
project      NONE                
department   defaultdepartment   
jobname      blast.pdb_derived   
jobnumber    2313760             
taskid       undefined
account      sge                 
priority     0                   
qsub_time    Fri Mar 27 22:06:53 2020
start_time   Fri Mar 27 22:06:57 2020
end_time     Fri Mar 27 22:07:37 2020
granted_pe   NONE                
slots        1                   
failed       0    
exit_status  0                   
ru_wallclock 40s
ru_utime     6.401s
ru_stime     1.181s
ru_maxrss    6.121KB
ru_ixrss     0.000B
ru_ismrss    0.000B
ru_idrss     0.000B
ru_isrss     0.000B
ru_minflt    3035                
ru_majflt    3                   
ru_nswap     0                   
ru_inblock   5968                
ru_oublock   424864              
ru_msgsnd    0                   
ru_msgrcv    0                   
ru_nsignals  0                   
ru_nvcsw     7048                
ru_nivcsw    184                 
cpu          7.582s
mem          29.088MBs
io           379.767MB
iow          0.000s
maxvmem      6.105MB
arid         undefined
ar_sub_time  undefined
category     -U banko,maiage,frangen -u banko -q maiage.q,short.q
</code></pre>

</div>

Cette commande vous donne accès à la mémoire utilisée par le job, son temps d'exécution, les informations sur le noeud, la queue... ainsi que son statut d'erreur.

### Interrompre un job lancé

Il est possible, pour différentes raisons, de vouloir interrompre un job soumis sur le cluster avec la commande `qdel`. Le numéro d'identifiant du job est utile pour cibler le job à interrompre.

<div class="example">
<p class="title">Interrompre le job 1995192</p>
<pre class="shell"><code>
[stage01@migale ~]$ qdel 1995192
stage01 has registered the job 1995192 for deletion
</code></pre>

L'utilisateur peut aussi interrompre tous ses jobs en spécifiant son identifiant avec l'option `-u`.

<p class="title">Interrompre tous les jobs soumis</p>
<pre class="shell"><code>
[stage01@migale ~]$ qdel -u stage01
stage01 has deleted job 1995285
stage01 has deleted job 1995286
stage01 has deleted job 1995287
</code></pre>

</div>

### Modifier un job en attente

La commande `qalter` permet de modifier des options de soumission _à la volée_, sans avoir besoin de relancer la commande `qsub`.

<div class="alert comment">Cette commande n'est valable que sur les jobs en attente.
</div>

<div class="example">
<p class="title">Changer la queue de soumission d'un job</p>
<pre class="shell"><code>
[stage01@migale ~]$ qalter -q short.q 2426996
modified hard queue list of job 2426996
</code></pre>
</div>

## Rechercher les ressources disponibles

La commande `qhost` permet de lister les ressources et de visualiser celles qui sont disponibles et celles qui sont occupées. L'option `-q` permet de lister les noeuds par queue.

Une représentation en temps réel de la charge du cluster est disponible sur la page d'accueil de notre site web : <a href="https://migale.inrae.fr">https://migale.inrae.fr</a>.

![Charge du cluster](../../load_cluster.png)

C'est à l'utilisateur de choisir les ressources souhaitées en fonction de ce qu'il souhaite faire.

<div class="example">
<p class="title">Je pense que mon job blast va prendre plus de 12 heures, mais moins de 72 heures. Blast est multithreadé et ne nécessite pas beaucoup de mémoire</p>

* Il faut choisir la queue `long.q`.

<pre class="shell"><code class="hljs lua">
[stage01@migale ~]$ qhost -q |grep -B 1 long.q
</code></pre>

* Il faut choisir parmi les noeuds proposés un noeud qui a beaucoup de CPUs disponibles

<pre class="shell"><code class="hljs lua">
...
n37                     lx-amd64       32    2   32   32 23.93  187.3G   14.1G   14.6G    1.5G
   long.q               BIP   0/12/32       
n38                     lx-amd64       32    2   32   32 32.01  187.3G    4.7G   14.6G    4.0G
   long.q               BIP   0/32/32       
n39                     lx-amd64       32    2   32   32 24.31  187.3G   27.4G   14.6G   14.6G
   long.q               BIP   0/26/32       
n40                     lx-amd64       32    2   32   32 22.57  187.3G    9.1G   14.6G    4.0G
   long.q               BIP   0/22/32       
n41                     lx-amd64       32    2   32   32 24.68  187.3G    8.9G   14.6G    4.1G
   long.q               BIP   0/27/32 
...
</code></pre>

Les noeuds 37 à 41 sont ceux qui ont le plus de CPUs disponibles (32). Actuellement, au maximum 20 CPUs sont disponibles sur le noeud `n37`. Sans attendre plus de ressources, l'utilisateur peut demander 20 CPUs au cluster et paramétrer le job en conséquence.

<pre class="shell"><code class="hljs lua">
[stage01@migale ~]$ qsub -cwd -V -N myblast -pe thread 20 -q long.q -l hostname=n37 -b y "conda activate blast-2.9.0 && blastn -db subject.fasta -query query.fasta -out out.blast -num_thread 20 && conda deactivate"
Your job 1995190 ("myblast") has been submitted
</code></pre>

</div>

## Créer une session interactive

La commande `qlogin` permet une connexion sur un noeud. Les options sont les mêmes que celles de la commande `qsub`.

Avantages :

* les ressources sont réservées le temps de la session

Inconvénients :

* La session est close à la fermeture de la connexion au serveur migale

<div class="example">
<p class="title">Lancer une session interactive avec 4 CPUs sur un noeud de la queue short.q</p>

<pre class="shell"><code class="">
[stage01@migale ~]$ qlogin -q short.q -pe thread 4
Your job 2426903 ("QLOGIN") has been submitted
waiting for interactive job to be scheduled ...
Your interactive job 2426903 has been successfully scheduled.
Establishing /opt/sge/util/resources/wrappers/qlogin_wrapper session to host n45 ...
The authenticity of host '[n45]:38610 ([192.168.1.45]:38610)' can't be established.
ECDSA key fingerprint is SHA256:LXzgn0wEAXL96PKdSaMrDxe1AYciZOzxl7ecGmrOJfs.
ECDSA key fingerprint is MD5:c3:98:13:54:1b:dd:64:35:08:5b:1f:98:b6:c3:85:dd.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[n45]:38610,[192.168.1.45]:38610' (ECDSA) to the list of known hosts.
stage01@n45's password: 
Last login: Thu Aug  8 16:06:26 2019 from nmigale
</code></pre>

</div>

La session interactive est considérée comme un job, elle a donc un identifiant et est visualisable avec la commande `qstat`.

<pre class="shell"><code class="hljs lua">
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
2426903 0.52079 QLOGIN     stage01         r     04/22/2020 11:38:18 short.q@n45                        4
</code></pre>

La commande pour quitter une session interactive est `exit`.

# Portail Galaxy

## Outils

## Données

## Utilisation

# Conclusions

Ce tutoriel avait pour objectif de vous familiariser avec l'infrastructure de la plateforme migale et à vous apprendre à utiliser le cluster de calcul.
Pour toute question supplémentaire, n'hésitez pas à nous envoyer un mail à <a href="mailto:help-migale@inrae.fr">help-migale@inrae.fr</a>.

À titre indicatif, les quelques questions suivantes vous permettront de vous auto-évaluer :

<div id="quiz">
  <div id="quiz-header">
    <p class="faded">Êtes-vous prêt à vous tester sur l'utilisation de l'infrastructure de Migale ?</p>
  </div>
  <div id="quiz-start-screen">
    <p><a href="#" id="quiz-start-btn" class="quiz-button">Commencer</a></p>
  </div>
</div>

<script>
$('#quiz').quiz({
  //resultsScreen: '#results-screen',
  //counter: false,
  //homeButton: '#custom-home',
  counterFormat: 'Question %current sur %total',
  questions: [
    {
      'q': 'Le serveur migale est accessible depuis Windows, MacOS et Unix',
      'options': [
        'Oui',
        'Non'
      ],
      'correctIndex': 0,
      'correctResponse': 'Bien sûr, avec le terminal pour Unix et MacOS, avec des outils comme putty ou MobaXterm pour Windows.',
      'incorrectResponse': 'Nous ne laissons personne de côté voyons !'
    },
    {
      'q': 'Si mon nom d'utilisateur est toto et mon groupe mygroup, quel est mon home directory ?',
      'options': [
        '/projet/mygroup/toto/work',
        '/projet/mygroup/save/toto',
        '/projet/mygroup/work/toto',
        '/projet/toto/work'
      ],
      'correctIndex': 1,
      'correctResponse': 'Bien ! Vous avez compris où se trouvent les home directories !',
      'incorrectResponse': 'Ah non, revisez le second chapitre, il est essentiel pour utiliser migale'
    },
    {
      'q': 'Je lance mes calculs directement sur le serveur migale',
      'options': [
        'Oui',
        'Non'
      ],
      'correctIndex': 1,
      'correctResponse': 'Bon réflexe ! Vous devez utiliser le cluster de calcul pour lancer vos analyses !',
      'incorrectResponse': 'Surtout pas ! Vous pouvez ralentir le système et gêner tous les autres utilisateurs'
    }
  ]
});
</script>


