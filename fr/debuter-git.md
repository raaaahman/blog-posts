# Se lancer dans le versioning avec Git

Dans le monde du développement, les applications connaissent un bon nombre de versions au cours de leur cycle de vie. Comment alors garder efficacemment l'historique et archiver les anciennes versions ? Bien sûr, on pourrait garder une collection de fichiers *.zip*, mais il y a une manière bien plus efficace de procéder, elle cette technique peut être appliquer à d'autres activités que le développement:

## Le versioning

Ou "versionnage" dans la langue de Michel Ancel, aussi appelé "contrôle des versions" ou "revision control". Bref, tous ces termes désigne un même procédé qui vise à déléguer la mémorisation des modifications d'un projet à un logiciel tiers. Ce logiciel est alors en mesure de fournir un historique desdites modifications, entre autres fonctionnalités utiles.

Comme ces logiciels doivent être manipulés par chaque contributeur à un projet, ils induisent par ce fait une certaine méthodologie qui doit être partagée au sein de l'équipe, et apprise par chacun des collaborateurs. Et je peux vous assurer que vous avez tout intérêt à vous y intéresser dès aujourd'hui afin d'en voir le plus rapidement les bénéfices, et ce, quel que soit votre niveau en programmation.

## Git

Git est le **système de contrôle des versions** lancé par *Linus Torvald*, il se différencie de ses concurrents par son approche **distribuée** du contrôle des versions. Cela implique, à l'inverse de l'approche *centralisée* choisie par *CVS* et *Subversion (svn)*, que chaque contributeur du projet dispose d'une copie complète du projet sur sa station de travail, et que chacune de ses copie est d'une importance égale. Ainsi, chaque modification apportée par un contributeur devra être transférée à chacun des autres contributeurs afin que tout le monde puisse être à jour sur les dernièers modifications. Pour cette raison, il est courant que les équipes utilisent un répertoire "principal", avec lequel chaque collaborateur se charge d'être à jour, mais ce n'est pas du tout rendu obligatoire par Git. Rappelez-vous simplement que chaque répertoire en vaut un autre et qu'il peut y en avoir autant que vous le désirez.

Comme il s'agit d'un projet de *Linus Torvald*, Git et de ce fait naturellement compatible avec toutes les distributions de *Linux*, et il est peut-être même déjà installé sur votre poste de travail. Si vous utilisez *Windows*, vous pouvez installer Git comme n'importe quel autre logiciel. Une fois fait, vous aurez la possibilité d'ouvrir un terminal nommé *Git Bash* qui imite l'interface en ligne de commande de Linux. Si vous ne vous y connaissez pas en commande Linux, pas de panique, les seules dont vous aurez besoin se résumeront à:
