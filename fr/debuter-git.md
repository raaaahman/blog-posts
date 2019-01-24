# Se lancer dans le versioning avec Git

Dans le monde du développement, les applications connaissent un bon nombre de versions au cours de leur cycle de vie. Comment alors garder efficacemment l'historique et archiver les anciennes versions ? Bien sûr, on pourrait garder une collection de fichiers *.zip*, mais il y a une manière bien plus efficace de procéder, elle cette technique peut être appliquer à d'autres activités que le développement:

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

Qu'est-ce que signifie `-m` suivi d'un message? Vous pourriez vous demander. Eh bien c'est un ... **message**. Ouais, c'est tout, simplement une message pour moi-même, afin de me rappeler ce que j'ai commité. Parce que j'ai maintenant deux *commits* dans mon projet, et qu'il y en aura, à terme, bien plus. Je ferais donc mieux de commencer à écrire ce que j'ai ajouté dans chaque commit. Je peux visualiser mon *historique* des commits dans mon terminal en tapant:

		log git

Et voilà ce que Git me montre:

    Commit b6a083df24f44af9d2fa6423108ae58669245297
    Auteur: raaaahman&lt;contact@devindetails.com>&lt;/contact@devindetails.com>
    Date: Lun Oct 15 12:35:44 2018 + 0200

    Nouveau chapitre «Persévérer avec Git»

    Commit 7aaca9131ea03d129380edc68f946e19d2c017d8
    Auteur: raaaahman&lt;contact@devindetails.com>&lt;/contact@devindetails.com>
    Date: Dim Oct 14 14:42:28 2018 + 0200

Passons en revue ce que nous avons ici. Il s'aGit d'une liste *de valida*tions, elle est triée par ordre décroissant de date. Pour chaqu*e comm*it vous avez plusieurs informations:




- C'est** SHA-1**: il s'aGit d'un identificateur unique pour cet*te vali*dation, il est généré automatiquement.
- Le n**om de l'**auteur et l'e-mail, afin que nous savons qui a commis les changements.
- Date **à laq**uelle les modifications ont été commises
- Finalement, le me**ssage qu**e l'auteur a écrit afin que n'importe qui peut savoir Whats ont été les changements sur



Pour le moment, il s'aGit d'un simple billet de blog écrit par un seul auteur et seulement deux validations ont été ajoutées. Je peux différer que chaque* commit* sera sur moi en ajoutant plus de texte à la poste et les choses seront simples et linéaires. Mais dans un projet plus vaste, avec de nombreuses fonctionnalités et plusieu*rs auteur*s, vous pouvez imaginer combien il est important que chaque au*teur doi*t écrire des messa**ges explicites chaque **fois qu'elle commet quelques changements, de sorte que ses collaborateurs n'auront pas à inspecter les fichiers pour savoir ce qui étaient les changements à propos.



Sur ce point, je ne pouvais pas résister à vous présenter l'ini<a href="https://www.conventionalcommits.org/en/v1.0.0-beta.2/">tiative des validations </a>conventionnelles, qui est une idée intéressante pour rationaliser et normaliser les messages de validation. Cela peut sembler un peu trop directive lorsque vous venez de commencer à écrire vos premièr*es valida*tions, mais vous pouvez rapidement voir les avantages de l'adopter à droite de la chauve-souris (ou vos collègues peuvent vous apprécier encore plus pour elle). Je vais essayer de vous donner un aperçu de ce dont il s'aGit:



Comme un article bien organisé, les mes*sages de la validation c*onventionnelle sont composés d'un en-t*ête, d'*un co*rps et* d'un pied* de pag*e. L'en-tête contient une étiquette qui indique le type** de **la validation et une brève descr**iption de ce** que cette validation est à propos. Le t*ype e*st un moyen rapide de catégoriser le type de travail qui ont été effectués, comme l'ajout d'une fonctionnalité, la correction d'un bug ou l'ajout de documentation au code existant, tandis que* la descript*ion indiquent où ce travail ont été appliqués et quelles modifications il introduit.



Fondamentalement, je peux arrêter mes messages de Commit à ce stade, et la plupart des messages de Commit devraient être ce court. Parce que Git est un Smart * * *, et il connaît déjà tous les changements que j'ai apportés à mon projet. Mais Git est crédule, et si je demande gentiment, il va m'afficher les changements. Je vais le demander comme ça:



		     Git show



Maintenant Git sortie dans mon terminal chaque changement que j'ai fait dans sa mode habituelle (qui est dit, les lignes supprimées commencent par un "-" et sont colorées en rouge, et les lignes ajoutées commencent par un "+" et sont colorées en vert, il montre également quelques lignes non modifiées juste pour donner un contexte autour de la  modifiés). Comme j'ai fait plusieurs corrections grammaticales ici et là, je ne peux pas vous montrer le journal entier, parce que c'est assez long, mais je vais vous donner un aperçu:



<figure class="wp-block-image"><img src="https://devindetails.com/wp-content/uploads/2019/01/start-Git-en-04_show.png" alt="" class="wp-image-92"/></figure>



OK, ça devrait faire pour un autre chapitre, alors devinez ce que je vais faire maintenant? Bien, je vais l'engager dans mon projet.



		    Git Add fr/Start-Git. MD
    Git commit-m "chapitre" Git va sur "terminé"



***Remar***q*ue: en tant que lecteur attentif, vous avez remarqué que je n'ai pas écrit mes messages de Commit en utilisant les conventions conventionnelles... Bien que je l'ai adopté dans mes projets de programmation, je pense qu'il fait n'est pas vraiment logique dans le contexte d'un blog. C'est une préférence et c'est habituellement quelque chose qui doit être discuté au sein d'une équipe. N'hésitez pas à lire un peu plus sur ces règles d'écriture, ils sont légers, mais je ne vous ai pas dit tous, ni ai-je énuméré tous leurs avantages.*



## Obtenir fantaisie



La dernière commande que j'ai utili`sé (Git sho`w) a été en mesure de me montrer le changement que j'ai fait dans mon dernier COMMIT. C'est une fonctionnalité cool, mais comme je vous ai montré dans une ancienn`e comman`de (Git log), le projet contient plus d'un commit, et j'ai ajouté un nouveau depuis que j'ai tapé ces commandes. Alors, comment puis-je voir ce que j'ai commis dans les précédentes validations?



Une solution serait de Git l`og mes `validations, copier le SH*A-1 (n*'oubliez pas, l'identificateur unique pour la validation) pour cette validation spécifique et puis collez-le à l`a command`e Git show, comme ceci:



		log Git
Git show 3bba4ec8f814f84ea8782f014b01da81e6cfabde



Et je peux voir tous les changements qui ont été commis dans ce commit. C'est l'utilité de l'identifica*teur *SHA-1, il est généré par Git et est assuré pour être absolument unique, de sorte que Git peut récupérer la validation spécifique, même si mon projet aurait contenu des milliers d'entre eux (et j'espère qu'il sera à l'avenir!).



Mais cette suite de nombres hexadécimaux est loin d'être facile à retenir par les êtres humains, ne trouvez-vous pas? (Oui, en notation hexadécimale, les lettres de «a» à «f» sont aussi des nombres!) Ne vous inquiétez pas, il existe des moyens plus simples pour récupérer les mêmes informations, comme cette commande:



		TÊTE de Show Git ~ 1



Ce que cela fait est qu'il va produire les modifications commises dans la validation précédant la dernière. Mais vous pouvez encore être confus par la syntaxe utilisée ici, n'est-ce pas? En fait, vous avez rencontré le quatrième objet fondamental de Git, qui est un REF (souven**ez-**vous que nous avons déjà des arb*res-st*ructures de dossiers-, blo*bs-fic*hiers binaires/texte-et les va*lidation*s). *REFS* n'existe pas vraiment par eux-mêmes, mais au lieu de cela, ils réfé**rencent un **autre objet Git afin que nous, les utilisateurs, peuvent accéder à ces objets avec une notation plus facile qu*e SHA-*1.



Le R*EF *H**EAD **est très utile, car il pointe essentiellement vers le dernier **COMMIT que vous avez fai**t.  Mais taper g`it show HEAD s`erait assez inutile, puisque Git mo`ntrent d`éjà la sortie de la dernière commit si aucun argument n'est passé à lui.



Ce que j'ai fait à la place a été de mentionner que je voulais aller un commit en arrière de la tête, qui est ce que la sy`nt`axe ~ 1 signifie. Vous avez probablement deviné que je peux revenir dans la mesure où mon projet contient des validations en tapan`t Git show HEAD ~ 2`, `Git montrer HEAD ~` 3, etc. Cela utile pour la comma`nde Git s`how, mais à une multitude d'autres commandes que je ne vais pas énumérer ici (principalement parce que je ne les connais pas tous ou très bien, et aussi parce que je ne peux pas vous enseigner la totalité de Git dans un seul billet de blog).



En parlant de la longueur du blog, je pense que vous pouvez avoir la quantité d'informations à traiter à ce point (ou peut-être je me sens paresseux pour écrire un peu plus), donc je vais vous laisser jouer avec cela pour l'instant. J'espère que je vous ai motivé à faire votre premier pas avec Git, parce que je pense que c'est un outil crucial dans un travail quotidien de développeur, et peut-être qu'il peut sauver quelques tracas pour d'autres emplois trop. Je peux écrire un peu plus à ce sujet, comme je suis loin d'avoir couvert même ses usages les plus communs dans ce poste unique, alors restez à l'écoute! Mais avant de partir, vous avez deviné ce que:



		    Git Add fr/Start-Git. MD
    Git commit-m "chapitre'obtenir fantaisie'fini"
