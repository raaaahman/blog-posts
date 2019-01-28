# Commencer à versionner avec Git

Dans le monde du développement, les applications connaissent un bon nombre de versions au cours de leur cycle de vie. Comment alors garder efficacement l'historique et archiver les anciennes versions ? Bien sûr, on pourrait garder une collection de fichiers *.zip*, mais il y a une manière bien plus efficace de procéder, elle cette technique peut être appliquer à d'autres activités que le développement:

## Le versioning

Ou "versionnage" dans la langue de Michel Ancel, aussi appelé "contrôle des versions" ou "revision control". Bref, tous ces termes désigne un même procédé qui vise à déléguer la mémorisation des modifications d'un projet à un logiciel tiers. Ce logiciel est alors en mesure de fournir un historique desdites modifications, entre autres fonctionnalités utiles.

Comme ces logiciels doivent être manipulés par chaque contributeur à un projet, ils induisent par ce fait une certaine méthodologie qui doit être partagée au sein de l'équipe, et apprise par chacun des collaborateurs. Et je peux vous assurer que vous avez tout intérêt à vous y intéresser dès aujourd'hui afin d'en voir le plus rapidement les bénéfices, et ce, quel que soit votre niveau en programmation.

## Git

Git est le **système de contrôle des versions** lancé par *Linus Torvald*, il se différencie de ses concurrents par son approche **distribuée** du contrôle des versions. Cela implique, à l'inverse de l'approche *centralisée* choisie par *CVS* et *Subversion (svn)*, que chaque contributeur du projet dispose d'une copie complète du projet sur sa station de travail, et que chacune de ces copies est d'une importance égale. Ainsi, chaque modification apportée par un contributeur devra être transférée à chacun des autres contributeurs afin que tout le monde puisse être à jour sur les dernières modifications. Pour cette raison, il est courant que les équipes utilisent un répertoire "principal", avec lequel chaque collaborateur se charge d'être à jour, mais ce n'est pas du tout rendu obligatoire par Git. Rappelez-vous simplement que chaque répertoire en vaut un autre et qu'il peut y en avoir autant que vous le désirez.

Comme il s'agit d'un projet de *Linus Torvald*, Git est de ce fait naturellement compatible avec toutes les distributions de *Linux*, et il est peut-être même déjà installé sur votre poste de travail. Si vous utilisez *Windows*, vous pouvez installer Git comme n'importe quel autre logiciel. Une fois fait, vous aurez la possibilité d'ouvrir un terminal nommé *Git Bash* qui imite l'interface en ligne de commande de Linux. Si vous ne vous y connaissez pas en commande Linux, pas de panique, les seules dont vous aurez besoin se résumeront à:

- `ls`: liste tous les fichiers et dossiers qui se trouvent dans le même dossier dans lequel vous vous trouvez actuellement (dans l'interface de ligne de commande, vous êtes toujours à l'intérieur d'un dossier de votre système)
- `cd mon_dossier` : remplace le dossier courant par le dossier nommé "mon_dossier" (dans cet exemple), ce dossier doit être à l'intérieur du dossier dans lequel vous vous trouvez actuellement
- `cd chemin/du/dossier`: fait la même chose, mais vous permet de naviguer à travers plusieurs dossiers dans une commande, dans l'exemple, nous allons finir dans le dossier "dossier", qui est à l'intérieur du dossier "du", qui est à son tour à l'intérieur du dossier "chemin".
- `cd ..` : Vous permet de vous déplacer dans le dossier parent à partir du dossier où vous vpius trouvez actuellement, vous pouvez le combiner dans un chemin d'accès, par exemple: `cd ../mon/dossier` qui vous déplacera dans le dossier parent du dossier dans lequel vous vous trouvez actuellement, puis à l'intérieur du dossier "mon", puis à l'intérieur du dossier "dossier"

Tout cela deviendra rapidement naturel après quelques errances à l'intérieur de vos dossiers. Il y a des outils qui se branchent sur Git pour lui donner une interface graphique, tels que *Git GUI* qui vient avec votre installation de Git sous Windows ou encore *GitKraken*, qui coûte quelques deniers, mais est réputé pour en valoir l'investissement. Cependant, vous devrez connaître le nom des commandes à exécuter dans tous les cas, il est donc préférable de commencer par la ligne de commande (en plus, vous pourrez vous prendre pour un hacker badass).

Je n'ai jamais utilisé Git sur un Mac (en fait, je n'ai jamais rien utilisé sur un Mac...) donc je ne vais pas vous expliquer comment l'installer, mais si vous avez trouvé cet obscur article d'un geek inconnu dans un coin sombre du Web, je vous fais confiance pour être en mesure de trouver un tutoriel d'installation dans des endroits plus reluisants de la toile.

## Initialiser un projet

Commençons par quelques notions de base. J'ai dit que vous pouvez appliquer le *contrôle de version* à d'autres activités que le développement, je vais utiliser mes billets de blog comme exemple.

La raison pour laquelle nous sommes en mesure d'utiliser Git avec du code source ou des publications en texte brut est que, ce dont Git se soucie, pourrait être résumé comme suit (dans le vocabulaire de Git):

- les *arbres* (dossiers): les parties structurantes du projet, les arbres contiennent d'autres arbres (sous-arbres) ou des ...
- ... *blobs* (fichiers): les parties du projet qui lui donne un but, les fichiers peuvent être soit binaires (images, vidéos, sons) ou des fichiers texte, mais Git fonctionne beaucoup mieux avec ces derniers.

Voici une représentation de la structure de mes dossiers:

    blog-posts
        |-fr
        || -un-article.md
        || -un-autre.md
        |-fr
        || -un-article-traduit.md

Je veux que Git suive la totalité de mes billets de blog, et je considère mon projet comme étant le blog lui-même et non chacun de ses billets. Pour ce faire, j'ouvre terminal/Git Bash dans le dossier "blog-posts" (vous pouvez le faire par un *clic droit > Git Bash / ouvrir dans la console* en général). Pour être sûr que je suis dans le bon dossier, je tape la commande `ls` et je dois voir mes deux sous-dossiers "en" et "fr". Ensuite, je démarre un projet Git avec la commande:

    git init

Le terminal m'informe que j'ai réussi à initialiser un projet Git, mais je ne vois pas de changements si je regarde dans mon explorateur de fichiers... C'est parce que tous les fichiers de Git ont été stockés dans un dossier caché nommé ".git". Pour le voir, je peux utiliser la commande `ls`, mais avec l'option `a`, donc je tape `ls -a`.

Ce dossier contient les données de Git liées à ce projet, dont une partie très importante de Git qui est *l'index*. Dans le temps, ce sera une copie complète de mon projet qui va répertorier tous les changements que je veux conserver, mais comme je viens d'initialiser mon *dépôt*, il est totalement vide. Je peux voir les différences entre la version sur laquelle je travaille, qui est appelée, selon les termes de Git, le *working tree* (ou parfois, le *working directory/répertoire de travail*) ainsi que l'*index*, en tapant la commande:

		git status

Oui, à l'heure actuelle, les deux *arbres* sont totalement différents. C'est normal car je viens d'initialiser un *dépôt* Git, parce que Git n'opère que lorsque je le lui demande, brave bête.

Vous vous demandez peut-être si garder une copie complète du projet est une bonne idée, n'est-ce pas? Nous devrions ainsi perdre énormément d'espace en dupliquant chaque projet comme celui-ci... Eh bien ne vous inquiétez pas pour cela, car tout ce qui se trouve dans le dossier ".git" est compressé pour optimiser l'espace et les fichiers sont vraiment légers (à part pour les fichiers *binaires*, comme les images). Et en fait, il y aura à terme, beaucoup de copies du projet que j'ai commencé à versionner! Voyons comment ça se passe:

## Travailler avec Git

OK, pour résumer ce dont nous avons parlé jusqu'ici, voici un petit schéma:

<div class="wp-block-image"><figure class="aligncenter"><img src="https://i2.wp.com/devindetails.com/wp-content/uploads/2019/01/start-Git_trees01.png?fit=860%2C385&amp;ssl=1" alt="" class="wp-image-96"/></figure></div>

Comme vous pouvez le voir, les deux arbres sont presque exactement les mêmes, sauf que, comme je suis en train d'écrire ce post, il apparaît dans le *répertoire de travail*. Cela fait un petit moment que j'ai commencé à rédiger cet article, je pense que je devrais stocker les modifications faites au projet en ce moment (en fait, j'aurais dû le faire dès que j'ai commencé à écrire).

Si j'utilise la commande `git status` à ce stade, Git m'informera qu'il a remarqué un nouveau fichier dans mon répertoire de travail (ou devrais-je dire, un nouveau *blob* dans mon *arbre de travail*). Pour propager la modification aux autres arbres, je dois d'abord informer l'*index* de ces modifications. Je vais donc taper:

		git add fr/start-Git.md

Maintenant, si `git status` à nouveau, Git m'informera que le fichier "start-git.md" a été ajouté à l'*index* et est prêt à être validé. Ce dernier mot aurait dû soulever votre curiosité, sinon vous ne faites pas attention, honte à vous! Alors concentrez-vous, parce que vous allez entendre ce mot dans presque toutes les lignes que vous allez lire sur Git à partir de ce point.

<figure class="wp-block-image"><img src="https://i0.wp.com/devindetails.com/wp-content/uploads/2019/01/start-Git_trees02.png?fit=860%2C354&amp;ssl=1" alt="" class="wp-image-97"/></figure>

Les *commits* sont les copies de votre projet que Git conserve pour vous. Vous pouvez les voir comme des "instantanés", une fois que vous avez *commité* votre travail, une nouvelle copie de votre projet est créée et celle-ci est *quasiment* immuable. Pour *commiter* (j'ai dit que vous allez entendre ce mot tout le temps!) mon travail, je tape:

    git commit

OK, je devrais expliquer cette commande un peu plus en détails: vous pouvez deviner maintenant ce à quoi le mot "commit" fait référence, même si vous ne réalisez pas tout ce qu'il implique, il suffit de se rappeler qu'il crée une copie de l'*index*. Donc, parce que j'ai ajouté mon fichier à l'*index* avec la commande précédente (rappelez-vous `git add`), git a compris ce que je veux *commiter* avec `git commit`.

<figure class="wp-block-image"><img src="https://i0.wp.com/devindetails.com/wp-content/uploads/2019/01/start-Git_trees03.png?fit=860%2C446&amp;ssl=1" alt="" class="wp-image-98"/></figure>

Comme vous êtes intelligent et attentif, vous avez réalisé que j'ai écrit un peu plus de texte entre le moment où j'ai ajouté des changements à l'*index*, et le moment où j'ai fait mon *commit*. Vous pensez probablement que ce texte n'a pas pu être ajouté dans le *commit*, puisque l'*index* n'a pas été mis à jour pour l'inclure... et vous avez tout à fait raison! Pour inspecter le contenu du dernier *commit*, je tape:

		git show

Ensuite, je peux lire les changements qui ont été *commité*, les lignes écrites en vert et précédées par un "+" sont des lignes qui ont été ajoutées, et celles écrites en rouge et précédé par un "-" sont des lignes qui ont été supprimées (le cas échéant). Si des lignes sont modifiées, Git considérera simplement qu'elles ont été supprimées et ajoutées à nouveau. Je ne vais pas vous montrer la sortie de mon terminal ici c'est exactement le contenu de cet article depuis le début jusqu'à `git add en/start-git.md`. Mais c'est ce que nous cherchions, les changements entre `git add en/start-git. md` et `git commit` ne sont pas présents dans le *commit*.

***Remarque :*** _lorsque vous utilisez `Git show`, votre terminal sera en mode lecture, ce qui vous permet de monter et descendre le document avec les flèches de votre clavier, vous pouvez quitter ce mode en appuyant sur "q"._

## Persévérer avec Git

Je parie que tout n'est pas clair pour vous en ce moment et vous pouvez avoir des questions qui restent sans réponse. Mais comme j'ai écrit encore un peu depuis mon dernier commit, je vais ajouter ces changements dans un nouveau commit:

		git add fr/start-git.md
    git commit -m "nouveau chapitre en cours"

Que signifie `-m` suivi d'un message? Eh bien c'est un ... **message**. Ouais... c'est tout, simplement une message pour moi-même, afin de me rappeler ce que j'ai commité. Parce que j'ai maintenant deux *commits* dans mon projet, et qu'il y en aura, à terme, bien plus. Je ferais donc mieux de commencer à écrire ce que j'ai ajouté dans chaque commit. Je peux visualiser mon *historique* des commits dans mon terminal en tapant:

		git log

Et voilà ce que Git me répond:

    Commit b6a083df24f44af9d2fa6423108ae58669245297
    Auteur: raaaahman&lt;contact@devindetails.com>&lt;/contact@devindetails.com>
    Date: Lun Oct 15 12:35:44 2018 + 0200

    Nouveau chapitre «Persévérer avec Git»

    Commit 7aaca9131ea03d129380edc68f946e19d2c017d8
    Auteur: raaaahman&lt;contact@devindetails.com>&lt;/contact@devindetails.com>
    Date: Dim Oct 14 14:42:28 2018 + 0200

Passons en revue ce que nous avons ici. Il s'agit d'une liste de *commits*, elle est triée par ordre décroissant de date. Pour chaque *commit* vous avez plusieurs informations:

- Le **SHA-1**: il s'agit d'un identifiant unique pour ce commit, il est généré automatiquement.
- Le pseudonyme de l'**auteur** du commit et son e-mail, afin que nous savons qui a effectué ces changements.
- La **date** à laquelle les modifications ont été commitées
- Finalement, le **message** que l'auteur a écrit afin que n'importe qui puisse savoir quels ont été les changements sur le projet

Pour le moment, il s'agit d'un simple billet de blog écrit par un seul auteur et seulement deux commits ont été ajoutées. Je peux imaginer que chaque *commit* correspondra simplement à un ajout de texte de ma part, ce qui sera très  linéaire. Mais dans un projet plus vaste, avec de nombreuses fonctionnalités et plusieurs *auteurs*, vous pouvez imaginer combien il est important que chaque *auteur* écrive des **messages explicites** chaque fois qu'il/elle commit des changements, de sorte que ses collaborateurs n'aient pas à inspecter les fichiers pour savoir ce dont il retourne.

Sur ce point, je ne pouvais pas résister à vous présenter l'initiative <a href="https://www.conventionalcommits.org/en/v1.0.0-beta.2/"> conventional commits </a>, qui est une idée intéressante pour rationaliser et normaliser les *messages* des commits. Cela peut sembler un peu trop directif si vous venez de commencer à écrire vos premiers commits, mais vous pouvez rapidement voir les avantages de l'adopter immédiatement (vos collègues peuvent également l'apprécier grandement). Je vais essayer de vous donner un aperçu de ce dont il s'agit:

Comme un article bien organisé, les messages au format *conventional commits* sont composés d'un **en-tête**, d'un **corps** et d'un **pied de page**. L'*en-tête* contient une étiquette qui indique le **type de commit** et une brève description de ce qu'a modifié ce commit. Le *type* est un moyen rapide de catégoriser le travail qui a été effectué, comme l'ajout d'une fonctionnalité, la correction d'un bug ou l'ajout de documentation au code existant, tandis que la *description* indique un peu mieux où ce travail a été appliqué et quelles modifications il introduit.

Fondamentalement, je pourrais arrêter mes *messages* de commit à ce stade, et la plupart des messages de commit devraient être aussi court. Parce que Git est un petit malin, et il connaît déjà tous les changements que j'ai apportés à mon projet. Mais Git est docile, et si je lui demande gentiment, il va m'afficher ces changements. Je vais le lui demander comme ça:

    git show

Maintenant Git imprime dans mon terminal chaque changement que j'ai fait de sa manière habituelle (c'est-à_dire, les lignes supprimées commencent par un "-" et sont colorées en rouge, et les lignes ajoutées commencent par un "+" et sont colorées en vert, il montre également quelques lignes non modifiées juste pour donner un contexte autour de celles  modifiées). Comme j'ai fait plusieurs corrections grammaticales ici et là, je ne vais pas vous montrer l'intégralité des logs, ce serait trop long, mais je vais vous tout de même vous montrer un aperçu:

<figure class="wp-block-image"><img src="https://devindetails.com/wp-content/uploads/2019/01/start-Git-en-04_show.png" alt="" class="wp-image-92"/></figure>

Bien, ça devrait suffire pour ce chapitre, vous devinez ce que je vais faire maintenant? Exact, je vais le commiter dans mon projet.

		git add fr/start-git.md
    git commit-m "chapitre 'Persévérer avec git' terminé"

***Remarque:*** _En tant que lecteur attentif, vous avez remarqué que je n'ai pas écrit mes messages de commit en utilisant les règles des conventional commits... Bien que je les ai adoptées dans mes projets de programmation, je pense qu'elles n'ont pas autant de sens dans le contexte d'un blog. C'est une préférence et c'est habituellement quelque chose qui doit être discuté au sein d'une équipe. N'hésitez pas à lire un peu plus sur ces règles d'écriture, elles sont légères, même s'il y a plus que ce que je vous ai brièvement résumés, et je n'ai pas non plus énuméré tous leurs avantages._

## Dompter Git

La dernière commande que j'ai utilisée (`git show`) a été en mesure de me montrer les changements que j'ai fait dans mon dernier commit. C'est une fonctionnalité pratique, mais comme je vous ai montré avec la commande précédente (`git log`), le projet contient plus d'un commit, et j'en ai ajouté un nouveau depuis que j'ai tapé ces commandes. Alors, comment puis-je voir ce que j'ai inclus dans mes précédents commits?

Une solution serait d'utiliser `git log`, copier le *SHA-1* (rappelez-vous, l'identifiant unique de chaque commit) d'un commit spécifique et puis de le coller après la commande `git show`, comme ceci:

		log git
    git show 3bba4ec8f814f84ea8782f014b01da81e6cfabde

Ainsi, je peux voir tous les changements qui ont été inclus dans ce commit. C'est l'utilité de l'identifiant *SHA-1*, il est généré par Git et est assuré d'être absolument unique, de sorte que Git puisse récupérer un commit spécifique, même si mon projet en avait contenu des milliers (et j'espère que ce sera le cas!).

Mais cette suite de chiffres hexadécimaux est loin d'être facile à retenir pour les êtres humains, n'est-ce pas? (Oui, en notation hexadécimale, les lettres de «a» à «f» sont aussi des chiffres!) Ne vous inquiétez pas, il existe des moyens plus simples pour récupérer les mêmes informations, comme cette commande:

		git show HEAD~1

Son effet est de montrer les modifications inclues dans l'avant-dernier commit. Peut-être êtes-vous perplexe devant la syntaxe utilisée ici? En fait, vous avez rencontré le quatrième objet fondamental de Git, qui est une **ref** (souvenez-vous, nous avions déjà des *arbres (tree)* -structures de dossiers-, les *blobs* -fichiers binaires/texte- et les *commits*). Les *refs* n'existe pas vraiment par elles-mêmes, mais au lieu de cela, elles **référencent** un autre objet Git afin que nous, les utilisateurs de Git, puissions accéder à ces objets avec une notation plus facile que le *SHA-1*.

La *ref* **HEAD** est très utile, car elle pointe vers le **dernier commit** ajouté au *dépôt*. Mais entrer `git show HEAD` serait assez inutile, puisque `git show` affiche déjà la sortie du dernier commit si aucun argument ne lui est passé.

A la place, j'ai indiqué à Git que je voulais aller un commit en arrière de ce *HEAD*, par le biais de syntaxe `~1`. Vous avez probablement deviné que je peux revenir en arrière d'autant de commits que je le souhaite (dans la mesure où mon projet en contient assez), en tapant `git show HEAD~2`, `git show HEAD~3`, etc. Si cela est utile pour la commande `Git show`, ça l'est également pour plusieurs autres commandes que je ne vais pas énumérer ici (principalement parce que je ne les connais ni toutes ni très bien, et aussi parce que je ne peux pas vous enseigner la totalité de Git dans un seul billet de blog).

En parlant de la longueur de cet article, je pense que vous devez déjà avoir une bonne quantité d'informations à assimiler à ce point (ou ne serait-ce qu'une excuse pour ne pas écrire plus?). Je vais donc vous laisser pratiquer ces quelques commandes pour l'instant. J'espère que je vous ai motivé à faire vos premiers pas avec Git, parce que je pense que c'est un outil crucial dans le travail quotidien du développeur, et peut-être qu'il pourra vous épargner quelques tracas. Evidemment, je suis loin d'avoir couvert ne serait-ce que les usages les plus communs de Git dans cet unique article, et j'en écrirais probablement d'avantage plus tard, alors restez à l'affût! Mais avant de partir, vous avez deviné ce que je vais faire:

    git add fr/start-git.md
    git commit -m "chapitre 'Dompter Git' terminé"
