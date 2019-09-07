# Les bases de Javascript

Plutôt qu'un tutoriel, cet article est une anti-sèche sur les fondamentaux du langage **JavaScript**. Je l'ai écrit quand j'étais moi-même débutant en programmation. J'ai essayé de le revisiter le plus légèrement possible afin de garder les formulations qui me paraissaient avoir du sens à l'époque, et qui je l'espère, parleront aux débutants.

## Table des matières

*   [JavaScript, qu'est-ce c'est?](#intro)
*   [Une brève histoire de JavaScript](#histoire)
*   [Jouons un peu avec JavaScript](#jouer)
*   [Les commentaires](#commentaires)
*   [Les variables et leurs types](#variables)
*   [Instructions et expressions](#instructions)
*   [Contexte et portée des variables](#contexte)
*   [Les conditions](#conditions)
*   [Les interrupteurs](#switch)
*   [Les boucles](#boucles)
*   [Les fonctions](#fonctions)
*   [Les tableaux](#tableaux)
*   [Les objets](#objets)

## (#intro) JavaScript, qu'est-ce c'est?

JavaScript est un **[langage de scripts](https://fr.wikipedia.org/wiki/Langage_de_script) [interprété](https://fr.wikipedia.org/wiki/Interpr%C3%A8te_(informatique))**. Son utilisation la plus courante est de créer des interactions au sein des pages web, des plus simples jusqu'à de véritables applications web. Il est aujourd’hui considéré comme le remplaçant du langage _Flash/ActionScript_ et profite de [frameworks](https://fr.wikipedia.org/wiki/Framework) très populaires comme AngularJS_ (développé chez Google), _ReactJS_ (développé chez Facebook), VueJS et bien d'autres...

L'environnement *Node.js* permet son utilisation [côté serveur](https://fr.wikipedia.org/wiki/Programmation_web#Programmation_web_c.C3.B4t.C3.A9_client) ainsi que comme outil d'*automatisation* des tâches par les développeurs.

## (#histoire) Une brève histoire de JavaScript

Développé en 1995 par *Brendan Eich* pour le compte de la société *Netscape* sous le nom de *LiveScript*, le langage est renommé *JavaScript* peu avant sa sortie, pour des raisons commerciales. Il est standardisé par l'*Ecma International* en 1997 et est depuis implémenté dans tous les navigateurs web. Bien qu'officiellement renommé *ECMAScript*, il reste mentionné majoritairement sous le nom de *JavaScript*.

Depuis lors, le langage ne cesse d'évoluer. Si l'*ECMA* rédige des nouvelles spécifications pour des versions officielles portant un numéro (*ECMAScript 5*, *ECMAScript 6*, etc.), cela reste aux fabricants des navigateurs internet d'implémenter les nouvelles fonctionnalités du langage. Ce qui fait que les fonctionnalités présentes **peuvent différer d'un navigateur à un autre**.

Le plus gros changement se produit en 2015 entre la version 5 et la 6 (*ES6*, nommée également *ES2015*). Si depuis lors la grande majorité des fonctionnalités ont été implémentées dans la quasi intégralité des navigateurs, il est courant de se poser la question de la compatibilité d'un code JavaScript avec un navigateur qui n'aurait pas été mis à jour depuis longtemps (comme cela peut exister dans les structures très procédurières comme les administrations).

**Note**: Cet article n'aborde que la syntaxe d'*ECMAScript 5*.

## (#jouer) Jouons un peu avec JavaScript

L'avantage que JavaScript soit interprété directement par le navigateur internet, c'est qu'on peut facilement tester du code à travers celui-ci. En ouvrant la console du navigateur (ouvrez le menu, cherchez un onglet développement ou outils>développement) il est possible d'écrire directement du code JavaScript qui sera directement exécuté. Faites par exemple quelques opérations mathématiques basique et le navigateur calculera les réponses tout seul

    			3 + 4 // trois plus quatre font sept
    			2 * 3 // deux fois trois font 6
    			7 - 5 // sept moins cinq est égal à deux
    			8 / 4 // huit que divise quatre est aussi égal à deux

Il est aussi possible d'utiliser la **fonction** (les fonctions seront abordées plus tard) `alert()` pour ouvrir une fenêtre en pop-up dans le navigateur.

    			alert("N'oubliez pas les guillemets")

## (#commentaires) Les commentaires

Puisque vous en allez en croiser souvent dans les paragraphes qui suivent, autant vous expliquez directement la notion de commentaires. Les commentaires sont des phrases écrites dans la langue du développeur (quoique que beaucoup préfèrent les écrire en anglais pour favoriser les échanges avec des développeurs du monde entier) qui ne sont pas lus par l'ordinateur lorsqu'il exécute le script. Cela a un intérêt pratique pour pouvoir se retrouver dans du code qui peut faire jusqu'à plusieurs milliers de lignes, et ils sont cruciaux dans un projet où plusieurs développeurs vont travailler sur le même code, car les manières d'arriver à un résultat donné peuvent varier selon les développeurs.

    			//Je suis un commentaire mono-ligne, j'aide les développeurs à comprendre leur code
    			je suis du texte perdu dans le code, je vais provoquer un erreur à la lecture du script
    			/*Je suis un commentaire multi-ligne
    			Je peux raconter ma vie sans limite de taille
    			et le navigateur n'en saura jamais rien!*/

### Le pseudo-code

Une pratique intéressante consiste à commencer par écrire uniquement des commentaires détaillant le code que le développeur va réaliser. Si cela peut paraître rébarbatif, cette pratique peut permettre de prévenir pas mal d'aller et retours dans le code vu qu'elle permet de réfléchir à l'ensemble du fonctionnement de celui-ci avant de s'attarder sur les détails techniques.

## (#variables) Les variables

Les variables servent à contenir des données. Chaque variable a un **nom** et une **valeur** d'un certain **type**.

### Déclaration de variables

La déclaration permet de créer une variable et éventuellement de lui associer une valeur (mais ce n'est pas obligatoire)

    			var chiffre = 1; //Une variable nommée "chiffre" contenant le nombre entier "1"
    			var vide; //Une variable nommée "vide" qui n'a pas de valeur associée

Comme l'on peut le voir une variable se **déclare** avec le mot clé `var` suivi de son nom puis éventuellement de la valeur qu'elle contient (précédée du signe "=").

### Nommage des variables

En JavaScript, les noms donnés aux variables peuvent contenir des lettres, des chiffres, des *underscores* ainsi que le symbole "$" et sont *sensibles à la casse*. Elles ne peuvent commencer par un chiffre. On privilégie la convention _Lower Camel Case_ qui consiste à écrire les ensemble de mots collés les uns aux autres, en utilisant une majuscule à chaque début de mot.

    			var MaVariable = "Je suis écrite en CamelCase";
    			var mavariable = "Pas moi";
    			var maVariable = "Moi, je suis écrite en lowerCamelCase";
    			//Notez que ces trois variables sont bien distinctes pour le navigateur, il faut les appeler en respectant leur casse
    			var comiquedu42 = "Tu ne serais pas plutôt écrite en dromedaryCase?"; //Ce terme existe aussi, mais il est moins courant...

**Note**: Il est impossible d'utiliser des caractères spéciaux, comme les lettres accentuées en français.

### Types de variables

La valeur contenue dans une variable sera d'un seul type, qui peut être soit un **nombre**, soit une **chaîne** de caractères, soit un **booléen** (une valeur primaire exprimé par les mot-clés `true` ou `false`).

    	    	var nombre = 8; //N'importe quel nombre entier ou décimal, positif ou négatif
    	    	var chaine = "Je suis une chaîne de caractère"; //Une simple lettre (voire juste un espace) ou un texte entier
    	    	//Notez qu'il est obligatoire d'écrire les guillemets (simples ou doubles) sans quoi JavaScript ne réalisera pas qu'il s'agit d'une chaîne de caractères
		var booleen = true; //Je suis un booléen, en Vrai

Comme dans la plupart des langages de script, les variables JavaScript seront du même type que la valeur qu'on leur assigne, on parle de **[typage dynamique](dictionnary.html#dynamic_typing)**. Les types de variables ne se mélangent pas, mais JavaScript peut faire une conversion de type dans le cas où l'on voudrait ajouter un chiffre à une chaîne de caractère.

    			var chiffre = 8;
    			var chaine = "On se voit le ";
    			var rdv = chaine + chiffre; // "On se voit le 8", la valeur contenue dans chiffre fait maintenant partie de la chaîne

    			var nombre = 23;
    			var secondNombre = "2";
    			var troisiemeNombre = nombre + secondNombre; // "232", JavaScript ne réalise que les conversions de nombres en chaîne, mais pas l'inverse!

### Appel de variables

Il est possible d'accéder au contenu d'une variable en écrivant simplement son nom dans le code sans aucun artifice.

    			var mot = "Palindrome";
    			alert(mot); //Affiche "Palindrome", qui est notre mot

## (#instructions) Instructions et expressions

JavaScript permet de traiter les données contenues dans ses variables via des opérateurs (arithmétiques, par exemple, car il y en d'autres):

    			var nb1 = 1, nb2 = 2;
    			var result = 0;
    			result = nb1 + nb2; //On additionne les nombres 1 et 2 contenus dans les variables
    			alert(result); //Affiche 3, le résultat de l'addition précédente

Cette **instruction** indique au navigateur qu'il faut effectuer une opération et va changer le résultat d'une des variables (ici ``result`), ce qu'il ne faut pas confondre avec une **expression**:

    			var nb1 = 1, nb2 = 2, result = 0; //Trois instructions, notez la syntaxe abrégée
    			
    			result == nb1 + nb2; 
    			/*Cette expression retourne le booléen false, 
    			car "result" est égal à zéro et nb1 + nb2 est égal à trois*/

Une expression ne modifie pas la valeur d'une variable, elle vérifie uniquement un état de fait au moment où elle est invoquée. Le résultat d'une expression est alors un **booléen** (soit `true`, soit `false`).

## (#conditions) Les conditions

Les conditions décident d'exécuter ou non des **blocs** de code selon la valeur d'une **expression**, dont elles attendent un résultat (donc sous forme de booléen, `true` ou `false`).

    	   		if (animal == "chat") {
    	   			alert(animal + " dit: miaouh...");
    	   	}

Si l'expression est fausse (retourne le booléen `false`), le bloc ne sera pas exécuté. Par contre, si la condition `if` est suivie d'une condition`else`, le bloc de code suivant sera exécuté.

    	   		if (animal == chat) {
    	   			alert(animal + " dit: miaouh...");
    	   		} else {
    	   			alert(animal + " dit: wouaf wouaf!");
    	   		}

Bon ce n'est pas très juste puisqu'il y a tout plein d'espèces animales autre que simplement les chats et les chiens. Dans ce cas, on peut enchaîner plusieurs blocs de conditions avec le mot clé `else if`:

    	   		if (animal == "chat") {
    	   			alert(animal + " dit: miaouh...");
    	   		} else if (animal == "chien") {
    	   			alert(animal + " dit: wouaf wouaf!");
    	   		}

Et on peut en enchaîner autant que l'on veut! Mais ce n'est pas toujours très pratique, alors...

## (#switch) Les interrupteurs

... on peut utiliser à la place un `switch`, qui est similaire à une série de conditions `if ... else if`:

    			switch (animal) {//On vérifie la valeur de la variable animal
    				case "chat": //Si notre animal est un chat
    					alert(animal + "dit: miaouh..."); //Alors il miaule
    					break; //Fin de l'instruction, les autres possibilité du switch ne sont pas vérifiées ni exécutées
    				case "chien": //Si notre animal est un chien...
    					alert(animal + "dit: wouaf! wouaf!");
    					break;
    				default: //Si notre animal ne correspond à aucune possibilité renseignée dans le switch
    				//alors c'est cette instruction qui sera exécutée
    					alert("Je ne connais pas cet animal");
    					break;
    			}//On ferme la bloc switch

Veillez à ne pas oublier d'utiliser l'instruction `break`, elle sert à **sortir du bloc** de code en cours (ici notre `switch`, regardez ou s'ouvre et se ferment les accolades). Si vous ne le faites pas, le navigateur exécutera toutes les instructions suivantes dans notre bloc, ce qui peut être fâcheux, mais qui peut également nous servir dans certains cas:

    			switch (animal) {
    				case "chat":
    				case "chien":
    				case "poisson rouge":
    					alert("C'est un animal de compagnie.");
    					break;
    				case "crocodile":
    				case "tigre":
    				case "rhinocéros":
    					alert("Ce n'est surtout pas un animal de compagnie!");
    					break;
    				default:
    					alert("Je ne connais pas cet animal");
    					break;
    			}

On voit ici que les trois premiers cas ("chat", "chien" et "poisson" ) aboutiront à l'exécution d'une même instruction. Et que les trois cas suivants ("crocodile", "tigre" et "rhinocéros") aboutiront également à l'exécution d'une instruction commune, mais différent de la précédente.

## (#boucles) Les boucles

### Boucles while

Les boucles permettent de répéter une instruction tant qu'une condition est vraie.

    	   		while (oxygen > 0) {
    	   			//Je peux respirer
    	   	}

Bon là notre boucle peut tourner pendant très longtemps, vu que l'oxygène sur terre se recycle, il y a donc risque de **boucle infinie**! Souvent, on utilise des variables pour compter le nombre d'itérations d'une boucle et l'arrêter après un certain nombre de tours.

		var distance = 500;
		while ( distance > 0) {
			//Je marche
			distance--; // Cette instruction décrémente la variable de 1 à chaque itération de boucle
		}

Dans l'exemple précédent, ma boucle tournera donc 500 fois, puis se terminera et le programme continuera l'exécution des instructions présentes après la boucle.

### Boucles for

Pour abréger la syntaxe précédente, on utilise généralement les boucles `for` :

    	   		for (var compteur = 0; compteur < 100; compteur++) { 
    	   		// Etape 1 : On déclare une variable
    	   		// Etape 2 : On assigne une condition à la boucle
    	   		// Etape 3 : On indique une action qui s'effectuera à chaque tour de boucle
    	   			alert(compteur); //Au premier tour l'alerte indiquera "1", au second "2", etc.
    	   		}

Notons que seule **cette deuxième étape est obligatoire**, on peut donc omettre la première et la dernière, ce qui nous ramène à la même utilité qu'une boucle `while`: 

    	   	for (; niveauMer < maVille;) {
    	   		//Je ne me noie pas
    	   	}

N'oubliez pas les point-virgules, sans quoi le programme ne comprendra pas que vous avez décidé de ne pas faire la première ni la dernière étape!

## (#contexte) Contexte et portée des variables

Quel que soit le langage de programmation, le code est toujours exécuté dans un **contexte** particulier.

### Le contexte global

En JavaScript, le code écrit directement sur la page est exécuté dans le **contexte global**, ce qui revient à exécuter les instructions de bout en bout jusqu'à la fin du code, sans restrictions particulières. Toutes les variables déclarées dans le contexte global sont accessibles à n'importe quel endroit du code, on dit de ces variables qu'elles ont une **portée globale**.

### Les blocs de code

Les conditions ou les boucles (entre autres) vont créer un nouveau contexte qui exécutera (ou non) du code, on parle de **bloc de code** et ces blocs sont entourés d'accolades.

    			var verite = true;
    			var laPalisse = "Alors tout va bien";
    			if (verite == true ) { //Début de bloc
    				alert(laPalisse);
    			} //Fin de bloc

En JavaScript, il n'y a pas vraiment de différence entre le code qui se trouve dans des **blocs de conditions ou des boucles** et du code qui se trouve dans le contexte global, les variables sont accessibles depuis le contexte global dans les blocs et depuis les blocs dans le contexte global. Seulement ce n'est plus vrai lorsqu'il s'agit de bloc de **fonctions**.

## (#fonctions) Les fonctions

Les fonctions permettent une réutilisation de blocs de code. Elles définissent **leur propre contexte** dans lequel des variables déclarées sont indépendantes du reste du code. On parle alors de **variables locales**.

    	    	var variableGlobale = 0;
    	    	
    	    function maFonction () {
	    	    	var variableLocale = 0; //On définit une variable qui sera utilisée uniquement dans la fonction
	    	    	variableLocale += 1; //On peut effectuer des opérations dessus une variable locale
	    	    	variableGlobale += 1; //On peut aussi effectuer une opération sur une variable déclarée hors de la fonction
	    	    	return variableLocale; //La fonction renvoie la valeur contenue dans sa variable locale
    	    }

L'instruction `return` interrompt l'exécution de la fonction et permet de récupérer une, et une seule **valeur**. Essayer d'utiliser le nom de la variable locale hors du bloc de la fonction pour récupérer la valeur qu'elle contient retournera une erreur. Pour utiliser cette valeur on fera alors un **appel** à la fonction:

    	    	maFonction(); //On appelle maFonction, qui s'exécute. Seulement sa valeur de retour n'est pas mémorisée.
    	    	var result = maFonction(); //Ici la variable result sera égale à la valeur que retourne maFonction, soit 1 (voir plus-haut)

En bref, on peut mettre le code que l'on veut dans une fonction, qui s'exécutera à chaque fois que l'on appellera cette même fonction. 

Il est important que de comprendre que le code présent dans une fonction sera exécuté **au moment de l'appel** de cette fonction, et non selon sa position dans votre fichier. Il faut bien donc faire attention à l'appeler au bon moment, comme par exemple:
 - au moment d'assigner son résultat à une variable
 - après la déclaration d'une variable globale qu'elle utilise
 - avant un bloc de code qui se sert de son résultat
 - etc.
 
Une autre syntaxe est possible:

		var incremente = function(1) {
			return nombre + 1;
		}

On constate que l'on a assigné la fonction à une variable. C'est également ce qu'a fait notre première fonction en réalité, même si JavaScript à fait cette opération pour nous. En fait, `incremente` comme `maFonction` ne sont pas des fonction elles-mêmes, mais des **références** qui permettent à JavaScript d'aller retrouver ces fonctions. C'est un sujet qui mériterait une explication approfondie, retenez pour l'instant que les deux syntaxes sont équivalentes.

### Les paramètres

Les fonctions peuvent inclure des **paramètres** (similaires à des variables locales) qui contiennent des valeurs sur laquelle la fonction va pouvoir opérer.

    	    	function maFonction (parametre1, parametre2) {
    	    		return parametre1 + parametre2;
    	    } //La fonction effectue une addition avec les deux nombres que l'on aura passé en paramètres

On peut donc utiliser cette fonction pour n'importe quelles valeurs que l'on veut additionner, par contre il faut faire attention à lui passer des paramètres du type qu'elle attend (ici, des nombres), sinon le résultat risque d'être... décevant.

## (#tableaux) Les tableaux

Les tableaux servent à contenir plusieurs données, potentiellement de plusieurs **types différents**. Ils agissent comme une série de variables, en quelque sorte.

    			var monTableau = ["Orange", "Banane", 4, true]; // Déclaration littérale d'un tableau avec 4 entrées

Un tableau comprend plusieurs **entrées** qui sont référencées par des **index** qui permettent d'accéder à leur contenu. Dans notre exemple précédent:

    			alert(monTableau[0]); //Affiche "Orange"
    			alert(monTableau[2]); //Affiche 4

On peut donc accéder aux différentes valeurs de notre tableau grâce à leur index qui représente leur position dans ce tableau. Attention, les tableau sont **indexés à partir de zéro**, ce qui signifie que la première entrée du tableau aura l'index "0", la seconde "1" et ainsi de suite... Également on peut tout à fait accéder à une entrée que l'on n'a as assignée (par exemple en entrant un index très grand) et le tableau retournera la valeur spéciale `undefined`.

### La propriété `length`

Il existe une **propriété** des tableaux dont l'on se sert très souvent qui est `length`, elle permet de retourner une valeur de type nombre qui correspond à **l'index le plus grand** plus 1.

    			alert(monTableau.length); //Affiche le nombre 4

Dans de nombreux cas cela correspond au nombre d'entrées du tableau, mais attention: si une entrée du tableau est vide, elle sera quand même comptabilisée, tant qu'il existe une entrée d'index plus grand! Exemple:

    			var nouveauTableau = ["rat", "lapin", "castor"]; //Un tableau à trois entrées
    			nouveauTableau[12] = "souris"; //On insère une nouvelle entrée plus loin dans le tableau
    			alert(nouveauTableau.length); //Affiche la valeur 13, puisque le plus grand index est 12!

## (#objets) Les objets

Les objets sont un autre type de conteneur de données, et ils sont extrêmement versatiles. Un objet se compose de plusieurs **propriétés**, qui peuvent être des variables, des tableaux, des fonctions (on parle alors de **méthodes**), voire même d'autres objets!

    			monObjet = {
    				variable1 : 2,
    				tableau1 : ["Chou", "Patate"],
    				sousObjet : {
    					sousVariable = "Salut"
    				}
    			}

On peut accéder à tout moment aux propriétés d'un objet global en renseignant son nom et le nom de cette propriété.

    			alert(monObjet.variable1); //Affiche 2, puisque c'est la valeur de la variable1 de monObjet
    			monObjet.tableau1[0] += "-fleur"; //Je modifie la valeur de l'entrée d'index 0 du tableau1 de monObjet
    			alert(monObjet.tableau1[0]); //Affiche "Chou-fleur", puisque j'ai modifié sa valeur à la ligne du dessus

### Les méthodes

Les méthodes sont des fonctions qui sont stockées en tant que propriétés d'un objet. 

		monObjet = {
			saPropriete = 1;
			saMethode = function() { //Déclaration de la méthode
				alert('Hello World!);
			}
		}

On les appelles de la même manière qu'une propriété.

		monObjet.saMethode(); //Affiche 'Hello World!'

Une fonction peut également être déclarée en dehors de l'objet, puis assignée ensuite en temps que propriété.

		function maFonction(nombre) {
			return nombre + 1;
		}
		
		monObjet = {
			saFonction : maFonction //Notez l'absence de parenthèse 
		}
		
		monObjet.saFonction(1) // Renvoie la valeur 2

Ce faisant, `maFonction` existe toujours dans le contexte global, et peut être appelée.

		maFonction(1) // Renvoie la valeur 2

C'est rarement ce que l'on cherche à faire, car l'utilisation d'objets permet au contraire la **séparation des responsabilités**, concept qui ne sera pas abordé ici, car il peut à lui seul remplir plusieurs livres.

### Le mot-clé this

A l'intérieur d'une fonction, le mot-clé `this` référence le **contexte d'exécution** de la fonction. Si cela vous paraît vague, retenez que son intérêt est surtout d'être appliqué au sein de méthodes, car le contexte dans ce cas, sera l'**objet** qui contient la méthode.

    			monObjet = {
    				variable : 5;
    				methode : function () { //On déclare la méthode
    					this.variable--;	// On applique une action sur la propriété de l'objet
    				}
    			}
    			
    			//On appelle maintenant la méthode
    			monObjet.saMethode();
    			alert(monObjet.variable1); //Affiche 4, puisque la méthode à décrémenté cette variable de 1
    			

Attention cependant, car `this` est assigné au moment de l'**appel** de la méthode, et non de sa déclaration. Cela peut éventuellement causer des problèmes dans des applications avec beaucoup d'objets qui contiennent d'autres objets. Là aussi, il y aurait beaucoup à dire sur le sujet et nous ne l'explorerons pas en détails dans cet article. Soyez simplement prévenus!

### Constructeurs

Un des intérêts des objets est de pouvoir les répliquer afin d'avoir que la structure soit la même, mais que les valeurs contenues dans leur propriétés changent. Il est possible de créer des objets grâce à une fonction que l'on appelle un **constructeur** ainsi qu'au mot-clé `new`.

		function Animal(nom, cri) {
			this.nom = nom;
			this.cri = cri;
		}
		
		var chien = new Animal('chien', 'ouaf');
		alert(chien.nom + ' dit : ' + chien.cri); // Affiche 'chien dit : ouaf'
		
		var chat = new Animal('chat', 'miaou');
		alert(chat.nom + ' dit : ' + chat.cri); // Affiche 'chat dit : miaou'

Dans ces cas, `this` correspond à l'objet qui sera retourné par la fonction (on parle d'**instanciation** de l'objet, aussi appelé **instance**). Notez que nous n'avons pas ici définit nous-même le retour de la fonction, c'est JavaScript qui fait ses tours de passe-passe en arrière-plan.

**Note** : Ce n'est en aucun cas obligatoire, mais très habituel de nommer les constructeurs en commençant par une majuscule. Cela donne un indice visuel pour les différencier d'autres fonctions.

### Prototypes

Le concept de **prototype** est central à JavaScript, et encore une fois, il faudrait le développer dans un article entier (au moins). Retenez simplement que de définir une méthode directement dans un *constructeur* va poser des problèmes pour utiliser le mot-clé `this` dans ces méthodes. On utilise alors le prototype de l'objet pour créer la méthode.

		function Animal(nom, cri) {
			this.nom = nom;
			this.cri = cri;
		}
		
		Animal.prototype.crier = function() {
			alert(this.cri);
		}
		
		var lion = new Animal('lion', 'roar');
		lion.crier(); // Affiche 'roar'

Encore une fois, ce sont les mécaniques internes de JavaScript qui permettent à tout cela de fonctionner, et je serai bien embêté si je devais vous expliquer en détails ce qui se passe en arrière-plan.

Toutefois est-il, lorsque je déclare la fonction `crier`, `this` dans ce cas se référera à l'**objet qui sera instancié** par le constructeur `Animal`. Il y a plusieurs manière d'arriver à ce résultat, notamment dans les nouvelles constructions syntaxiques introduites par *ES6*, mais le but n'est pas d'être exhaustif ici, car les objets et prototypes sont en réalité présents à tous les niveaux de JavaScript que nous avons vu jusqu'ici. 

Cela pourrait être le sujet d'un autre article...