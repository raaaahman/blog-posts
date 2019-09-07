
Pendant le *WordCamp Paris 2019*, il y a eu beaucoup de conférences que vous serez bientôt en mesure de pouvoir visionner sur *wordpress.tv*. Il y a eu en parallèle de ces conférences, des discussions plus informelles et non enregistrées, durant lesquelles les participants, assis dans des canapés et sur des chaises autour de tables basses, ont discuté de sujets prédéfinis, sous l'oeil bienveillant d'un animateur.

Je tiens à vous faire un retour de l'une de ces "causeries", ayant trouvé les échanges très informatifs. Le sujet de cette causerie était la sécurité dans WordPress, et notre coordinateur était [Julio Potier](https://profiles.wordpress.org/juliobox/), fondateur de l'extension [SecuPress](http://secupress.pro/), directeur de l'association *WPFR*, et consultant *WordPress* spécialisé en sécurité pendant des années (entre autres rôles...). Inutile de préciser que nous avons tous eu beaucoup de questions à lui poser.

## La communauté WordPress, notre plus grand atout

Un point que Julio a mentioné immédiatement est l'importance de notre communauté, et comment elle nous fournit à tous un important flux de connaissances sur les attaques et les moyens de défense avec notre outil commun, *WordPress*. En effet, si la grande part de sites Web motorisés par *WordPress* peut attirer beaucoup de pirates, elle a également aidé à développer, au cours des années, un grand réseau de professionnels **partageant leurs connaissances**, soit librement, soit en tant que consultants. Nous ne sommes pas seuls dans cette tâche, et Julio n’a pas manqué une occasion de nous rappeler ce fait pendant toute la conversation.

Un autre grand avantage de l’utilisation d’un tel outil populaire et ouvert, est que **les mises à jour sont fréquentes**. Cela signifie que les failles nouvellement trouvées peuvent être résolues rapidement. En effet, tout le monde peut parcourir le code ou peut faire quelques tests de son côté, puis signaler la faille de sécurité découverte; voire même essayer de la corriger, et soumettre une demande de modification sur le noyau de *WordPress*.

## Les extensions de sécurité sont-elles suffisantes?

Une question qui a été rapidement posée, est l’utilité des extensions de sécurité, et plus précisément, de leurs différentes versions (gratuites ou payantes). Il en existe plusieurs dans l'écosystème *WordPress*, et elles semblent beaucoup utilisées par la communauté, mais avons-nous besoin de toutes les fonctionnalités d’une extension "Pro" (comprendre: payante)?

La réponse de Julio est: «cela dépend du site Web que vous construisez». En effet, de l’outil de blogs simple qu'était *WordPress*  à ses débuts, il a évolué pour être utilisé à de nombreuses fins de nos jours. Tous les sites varient grandement en fonctionnalités, et ces différentes fonctionnalités peuvent nécessiter plusieurs protections différentes. Vous construisez un site e-commerce? Cela signifie que vous allez avoir besoin de récolter des données personnelles de vos utilisateurs, et vous devrez bien les protéger! Vous bloguez? Mieux vaut être sûr que vous ne serez pas spammé dans les commentaires, etc.

Il n’y a pas de solution unique quand il s’agit de sécurité, et le plus efficace sera toujours de demander un audit à quelqu’un ayant une expérience dans la sécurité Web ou le type de site Web que vous construisez, voire mieux, à une **personne expérimentée** dans les deux domaines!

## Les extensions, portes dérobées potentielles pour les pirates

En parlant d'extensions, *WordPress* croule littéralement sous leur nombre, et je ne suis pas sûr que nous soyions en mesure de trouver quelque part un site WordPress n'utilisant absolument aucune de ces extensions. Malheureusement, elles sont la principale façon dont les pirates peuvent pénétrer nos sites. Cela peut être expliqué assez facilement, car les équipes de développement d'extensions, tout comme leurs contributeurs, ne sont pas aussi nombreux que ceux travaillant sur le noyau de *WordPress*, et chacun d’entre eux n’est pas nécessairement un développeur expérimenté non plus. Alors comment pouvons-nous nous protéger contre de telles **vulnérabilités**? 

La première réponse est, encore une fois, de s’appuyer sur la  communauté. Les nouvelles se propagent rapidement, et en faisant de la  **veille régulière**, vous pourriez avoir connaissance de failles  nouvellement trouvées avant qu'elles ne soient exploitées sur vos sites.  Les informations sur cette question ne sont pas difficiles à trouver,  soit sur le blog wordpress.org, qui a une [étiquette "sécurité"](https://wordpress.org/news/category/security/) pour cette question, le site communautaire [WP Vuln DB](https://wpvulndb.com/) ou même les blogs des différentes extensions de sécurité pourraient être très utiles (comme le [blog de SecuPress](https://secupress.me/fr/blog/), par exemple).

Un autre grand avantage de notre communauté très active, est la fréquence des mises à jour. Alors assurez-vous de **mettre à jour** vos sites Web à la dernière version de *WordPress*, et de chacune de vos extensions. Faites-le sur un environnement de test en premier lieu, comme vous ne pouvez pas être sûr que toutes vos extensions soient déjà compatibles; même si elles disent avoir été testées avec cette dernière mise à jour, elles pourraient avoir été modifiées d’une manière qui peut ne pas  totalement être en adéquation avec votre site.

Mais ce n'est pas tout, car en étant une grande communauté d’utilisateurs, nous pouvons facilement distinguer les extensions populaires dans l’écosystème *WordPress*, et cela aide grandement à savoir si l'on peut **faire confiance** ou non à une certaine extension. En effet, les utilisateurs ne vont pas conserver une extension qui rendrait leurs sites vulnérables. En outre, les attaquants vont probablement viser les plugins les plus utilisés, afin de pouvoir cibler le plus de sites possible. Donc, si vous n’aviez pas entendu parler d’une attaque sur une extension avec un demi-million d’installations actives, cette extension est probablement suffisamment sécurisée.

## Notre responsabilité en tant que développeurs de plugins

Comme dans le paragraphe précédent, la défense principale contre tout type d’attaque, est d’être conscient de leur éventualité. C’est donc une bonne habitude dde **faire de la veille** sur la sécurité, ou même le développement *WordPress* en général. Il ne s’agit pas seulement de bulletins de blogs, vous pouvez également lire du code! Vous voulez implémenter une nouvelle fonctionnalité? Plusieurs extensions doivent  potentiellement déjà faire quasiment la même chose, et leur code sera probablement *open source*, alors n’hésitez pas à prendre l’exemple sur celles-ci. Dans ce cas, préférez les extensions largement utilisées et bien connues, comme *WooCommerce*, par exemple.

En parlant de fonctionnalités, certaines sont évidemment **plus risquées** que d’autres. Fondamentalement, tout ce qui insère des informations dans la base de données doit être méticuleusement vérifié. Mais pas seulement, chaque fois que vous lisez des informations à partir d’une URL, ou à partir d’un formulaire, des attaquants pourraient essayer d’y injecter du code. C’est ce qui s’est passé récemment, avec *Easy SMTP*, comme discuté sur le blog de [WordFence](https://www.wordfence.com/blog/2019/03/hackers-abusing-recently-patched-vulnerability-in-easy-wp-smtp-plugin/). Je ne vais pas énumérer tous les types de vulnérabilités qui peuvent découler de nos développements, car ce n’est pas l’objectif de cet article, (et je ne suis pas un expert dans le domaine non plus) mais sachez que la liste tenue à jour annuellement par la fondation *OWASP* , appelée [Top Ten Project](https://www.wordfence.com/blog/2019/03/hackers-abusing-recently-patched-vulnerability-in-easy-wp-smtp-plugin/), recense justement les failles de sécurités les plus exploitées sur nos sites (et pas uniquement ceux propulsés par *WordPress*).

Heureusement, il ya une très grande chance pour que *WordPress* aie déjà créé des fonctions pour l’utilisation que vous planifiez. Ces fonctions sont déjà sécurisées, donc vous feriez mieux d'**utiliser ces fonctions** au lieu de réinventer la roue. Une fois de plus, n’hésitez pas à rechercher dans le noyau de *WordPress*, ou le code d’autres extensions pour trouver ce dont vous avez besoin. Et, comme *WordPress* est une communauté ouverte, vous pourriez être bien guidés en demandant de l’aide sur les forums.

Il y a aussi un outil utilisé pour vérifier que votre code est conforme aux normes de *WordPress* (un *sniffer*), appelé [WPCS](https://packagist.org/packages/wp-coding-standards/wpcs#user-content-introduction), qui vous avertira également des failles de sécurité potentielles dans votre code. Il aide en effet, mais ce n’est pas une solution ultime, surtout lorsque vous commencez à insérer des annotations dans votre code pour qu’il ignore certains faux-positifs (une fonctionnalité de* WPCS*). Ne vous abstenez pas de demander à d’autres développeurs des revues de code, car un **œil expérimenté** pourrait remarquer quelque chose qu’une machine aurait laissé passer. Encore une fois, avec la taille de notre communauté, vous avez le choix pour chercher une telle aide: votre entreprise, les forums, les rencontres et conférences, des espaces de co-working...

## Avoir un plan B, une considération obligatoire

Éventuellement, nous devons être préparés à ce que toutes nos mesures de sécurité ne suffisent pas. Être piraté est une probabilité que nous devons tous accepter lorsque nous décidons d’héberger notre contenu sur le Web.

La mesure la plus évidente est d’avoir une **sauvegarde** de votre base de données. Certains fournisseurs d’hébergement font une copie régulière de vos bases de données, voire même de votre système de fichiers, mais vous pouvez le faire par vous-même également. Il existe des extensions dédiés à l’exportation ou à la mise en ligne de sauvegardes de votre base de données, essayez quelques solutions et trouvez celle qui vous convient le mieux.

Mais ce ne sont pas les seules données que vous souhaitez sauvegarder, vous devriez peut-être vous protéger de la perte de vos fichiers médias également (images, documents PDF et similaires), ainsi que des développements que vous avez codé. Là encore, il y a plusieurs solutions, comme d’avoir vos images stockées en ligne, de *versionner* de votre code, etc. Manuellement ou en utilisant une extension de *WordPress*.

Cela peut être négligé par certaines personnes, mais avoir un **site de test** distinct de votre site public, en dehors de l’utilité qu’il apporte lors du développement, peut également vous aider à revenir en jeu très rapidement, vu que vous n'auriez qu'à faire une copie de ce site puis de l'envoyer sur votre hébergement public. Enfin, vous aurez à résoudre les problèmes liés à votre serveur d’abord, évidemment.

Peut-être qu'il y a beaucoup de sujets discutés ci-dessus avec lesquels vous n’êtes pas familier, et il n’y a pas de honte à l’admettre. En fait, cette discussion m’a ouvert les yeux sur de bonnes pratiques que je ne mets pas en place, ainsi que certains domains dans lesquels je suis plutôt faible. C’est normal, personne ne peut tout connaître à elle seule, mais heureusement nous ne sommes pas seul dans cette entreprise! Ainsi, un dernier conseil est de **garder contact** avec des personnes spécialisées - des amis, des connaissances, des collègues de travail - qui pourraient vous aider à corriger votre site Web sur les points pour lesquels n’êtes pas très confiants. Soyez prêts à payer ces services si vous en trouvez le besoin. Et si vous hésitez, posez-vous la question de combien un moment d’arrêt sur votre serveur, ou une fuite de données, vous coûterait à la place...

## Résumé

Il y a eu pas mal pistes exposées dans cet article, et certaines peuvent vous paraître encore obscures (même si j’espère que je vous ai donné envie de vous renseigner). Si je devais résumer, je le ferai en trois mots: l**ire, demander, rapporter**. 

La communauté est ce qui peut vraiment nous sortir de nos ennuis. En partageant nos connaissances et notre expérience, chacun de nous peut devenir plus fort et nous pouvons renforcer nos outils et processus également. Trouvez donc une bonne source d’information, restez à l’écoute et apportez votre contribution. Dans ce cas, on se croisera probablement!