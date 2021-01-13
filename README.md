# Les bonnes pratiques en Ruby

## La conception de classes et méthodes en Ruby

D'apres [Sandi Metz'](http://rubyrogues.com/087-rr-book-clubpractical-object-oriented-design-in-ruby-with-sandi-metz/) :

  1. Une classe ne doit pas dépasser **100 lignes** de code.
  2. Une méthode ne doit pas dépasser **5 lignes** de code.
  3. Une méthode ne doit pas avoir plus de **4 paramètres**. [¹](#source-1)
  4. Un controlleur doit instancier **1 seul objet**. [²](#source-2)

*<a name="source-1">¹</a> Hash comprit*\
*<a name="source-2">²</a> Utiliser le pattern **Facade** ou **Présenteur*</a>**

## Le principe S.O.L.I.D

### Responsabilité unique (Single responsibility principle)
Une seule responsabilité pour une classe ou une méthode.

Prenons l'exemple d'un module qui compile et imprime un rapport. Imaginons que ce module peut changer pour deux raisons. D'abord, le contenu du rapport peut changer. Ensuite, le format du rapport peut changer. Ces deux choses changent pour des causes différentes; l'une substantielle, et l'autre cosmétique. Le principe de responsabilité unique dit que ces deux aspects du problème ont deux responsabilités distinctes, et devraient donc être dans des classes ou des modules séparés. Ce serait une mauvaise conception de coupler ces deux choses dans une même classe.

La raison pour laquelle il est important de garder une classe axée sur une seule préoccupation est que cela rend la classe plus robuste. En continuant avec l'exemple précédent, s'il y a un changement dans le processus de compilation du rapport, il y a un plus grand danger que le code d'impression se casse si elle fait partie de la même classe.

La responsabilité est définie comme une tâche assignée à un acteur unique2

### Ouvert/fermé (Open/closed principle)
Une entité applicative (class, method, module ...) doit être **ouverte à l'extension**, mais **fermée à la modification**.

En programmation orientée objet, le principe ouvert/fermé (open/closed principle) affirme qu'une classe doit être à la fois ouverte (à l'extension) et fermée (à la modification). Il correspond au « O » de l'acronyme SOLID. « Ouverte » signifie qu'elle a la capacité d'être étendue. « Fermée » signifie qu'elle ne peut être modifiée que par extension, sans modification de son code source.

L'idée est qu'une fois qu'une classe a été approuvée via des revues de code, des tests unitaires et d'autres procédures de qualification, elle ne doit plus être modifiée mais seulement étendue.

En pratique, le principe ouvert/fermé oblige à faire bon usage de l'abstraction et du polymorphisme.

### Substitution de Liskov (Liskov substitution principle)
Une instance de type T doit pouvoir être remplacée par une instance de type G, tel que G sous-type de T, sans que cela ne modifie la cohérence du programme.

#### Principe
Le principe de Liskov impose des restrictions sur les signatures sur la définition des sous-types :

- Contravariance des arguments de méthode dans le sous-type.
- Covariance du type de retour dans le sous-type.
- Aucune nouvelle exception ne doit être générée par la méthode du sous-type, sauf si celles-ci sont elles-mêmes des sous-types des exceptions levées par la méthode du supertype.

On définit également un certain nombre de conditions comportementales (voir la section Conception par contrat).

#### Conception par contrat
Le principe de substitution de Liskov est étroitement relié à la méthodologie de programmation par contrat aboutissant à des restrictions qui spécifient la manière dont les contrats peuvent interagir avec les mécanismes d'héritage :

- Les préconditions ne peuvent pas être renforcées dans une sous-classe. Cela signifie que vous ne pouvez pas avoir une sous-classe avec des préconditions plus fortes que celles de sa superclasse ;
- Les postconditions ne peuvent pas être affaiblies dans une sous-classe. Cela signifie que vous ne pouvez pas avoir une sous-classe avec des postconditions plus faibles que celles de sa superclasse.

De plus, le principe de substitution de Liskov implique que des exceptions d'un type nouveau ne peuvent pas être levées par des méthodes de la sous-classe, sauf si ces exceptions sont elles-mêmes des sous-types des exceptions lancées par les méthodes de la superclasse.

Une fonction utilisant la connaissance de la hiérarchie de classe viole le principe car elle utilise une référence à la classe de base, mais doit aussi avoir connaissance des sous-classes. Une telle fonction viole le principe ouvert/fermé car elle doit être modifiée quand on crée une classe dérivée de la classe de base.

### Ségrégation des interfaces (Interface segregation principle)
Plusieurs interfaces spécifiques pour chaque client plutôt qu'une seule interface générale.
Aucun client ne devrait dépendre de méthodes qu'il n'utilise pas. 
Il faut donc diviser les interfaces volumineuses en plus petites plus spécifiques, de sorte que les clients n'ont accès qu'aux méthodes intéressantes pour eux. Ces interfaces rétrécies sont également appelés interfaces de rôle.
Tout ceci est destiné à maintenir un système à couplage faible, donc plus facile à refactoriser.

### Inversion des dépendances (Dependency inversion principle)
Il faut dépendre des abstractions, pas des implémentations
Les deux assertions de ce principe sont :

- Les modules de haut niveau ne doivent pas dépendre des modules de bas niveau. Les deux doivent dépendre d'abstractions.
- Les abstractions ne doivent pas dépendre des détails. Les détails doivent dépendre des abstractions.

[Source](https://fr.wikipedia.org/wiki/SOLID_(informatique))

## Les Design Patterns

D'après le Gang des quatres (Gang of Four) il existe plusieurs types de patterns dans la conception de logiciels orientée objet :

### Les patterns de création (Creational Pattern)
Le premier type de motif est le motif de création. Les motifs de création permettent d'instancier des objets individuels ou des groupes d'objets liés. Il existe cinq modèles de ce type :

#### Abstract Factory (Usine abstraite)
Le modèle d'usine abstraite est utilisé pour fournir à un client un ensemble d'objets liés ou dépendants. Les "familles" d'objets créées par la fabrique sont déterminées au moment de l'exécution.

#### Builder (Constructeur)
Le modèle builder est utilisé pour créer des objets complexes avec des parties constitutives qui doivent être créées dans le même ordre ou en utilisant un algorithme spécifique. Une classe externe contrôle l'algorithme de construction.

#### Factory Method (Méthode de l'usine)
Le modèle d'usine est utilisé pour remplacer les constructeurs de classe, en abstraction du processus de génération d'objets afin que le type de l'objet instancié puisse être déterminé au moment de l'exécution.

#### Prototype (Prototype)
Le modèle prototype est utilisé pour instancier un nouvel objet en copiant toutes les propriétés d'un objet existant, créant ainsi un clone indépendant. Cette pratique est particulièrement utile lorsque la construction d'un nouvel objet est inefficace.

#### Singleton (Singleton)
Le modèle singleton garantit qu'un seul objet d'une classe particulière est créé. Toutes les autres références aux objets de la classe singleton se rapportent à la même instance sous-jacente.

### Structural Patterns (Modèles structurels)
Le deuxième type de modèle de conception est le modèle structurel. Les modèles structurels permettent de définir les relations entre les classes ou les objets.

#### Adapter (Adaptateur)
Le modèle d'adaptateur est utilisé pour fournir un lien entre deux types autrement incompatibles en enveloppant l'"adaptateur" avec une classe qui prend en charge l'interface requise par le client.

#### Bridge (Pont)
Le modèle de pont est utilisé pour séparer les éléments abstraits d'une classe des détails de l'implémentation, fournissant ainsi le moyen de remplacer les détails de l'implémentation sans modifier l'abstraction.

#### Composite (Composite)
Le modèle composite est utilisé pour créer des structures arborescentes hiérarchiques et récursives d'objets apparentés où tout élément de la structure peut être accessible et utilisé de manière standard.

#### Decorator (Décorateur)
Le motif décorateur est utilisé pour étendre ou modifier la fonctionnalité des objets en cours d'exécution en les enveloppant dans un objet d'une classe décorateur. Cela offre une alternative flexible à l'utilisation de l'héritage pour modifier le comportement.

#### Facade (Façade)
Le modèle de façade est utilisé pour définir une interface simplifiée vers un sous-système plus complexe.

#### Flyweight (Masse volante)
Le modèle de poids mouche est utilisé pour réduire l'utilisation de la mémoire et des ressources pour des modèles complexes contenant plusieurs centaines, milliers ou centaines de milliers d'objets similaires.

#### Proxy (Proxy)
Le modèle de proxy est utilisé pour fournir un objet de substitution ou de remplacement, qui fait référence à un objet sous-jacent. Le proxy fournit la même interface publique que la classe de sujets sous-jacente, ajoutant un niveau d'indirection en acceptant les requêtes d'un objet client et en les transmettant à l'objet sujet réel si nécessaire.

### Les patterns de comportement (Behavioural Patterns)
Le dernier type de modèle de conception est le modèle comportemental. Les modèles comportementaux définissent les modes de communication entre les classes et les objets.

#### Chain of Responsibility (Chaîne de responsabilité)
Le modèle de chaîne de responsabilité est utilisé pour traiter des demandes variées, chacune d'entre elles pouvant être traitée par un gestionnaire différent.

#### Command (Commandement)
Le modèle de commande est utilisé pour exprimer une demande, y compris l'appel à effectuer et tous ses paramètres requis, dans un objet de commande. La commande peut ensuite être exécutée immédiatement ou conservée pour une utilisation ultérieure.

#### Interpreter (Interprète)
Le modèle d'interprétation est utilisé pour définir la grammaire des instructions qui font partie d'une langue ou d'une notation, tout en permettant d'étendre facilement la grammaire.

#### Iterator (Itérateur)
Le modèle d'itérateur est utilisé pour fournir une interface standard permettant de parcourir une collection d'éléments dans un objet global sans avoir besoin de comprendre sa structure sous-jacente.

#### Mediator (Médiateur)
Le modèle de médiateur est utilisé pour réduire le couplage entre les classes qui communiquent entre elles. Au lieu que les classes communiquent directement, et nécessitent donc une connaissance de leur mise en œuvre, les classes envoient des messages via un objet médiateur.

#### Memento (Mémento)
Le modèle memento est utilisé pour capturer l'état actuel d'un objet et le stocker de manière à ce qu'il puisse être restauré ultérieurement sans enfreindre les règles d'encapsulation.

#### Observer (Observateur)
Le modèle observateur est utilisé pour permettre à un objet de publier les changements de son état. Les autres objets s'abonnent pour être immédiatement informés de toute modification.

#### State (État)
Le modèle d'état est utilisé pour modifier le comportement d'un objet lorsque son état interne change. Le modèle permet à la classe d'un objet de changer apparemment au moment de l'exécution.

#### Strategy (Stratégie)
Le modèle de stratégie est utilisé pour créer une famille d'algorithmes interchangeables à partir de laquelle le processus requis est choisi au moment de l'exécution.

#### Template Method (Méthode du modèle)
Le modèle de la méthode des modèles est utilisé pour définir les étapes de base d'un algorithme et permettre la modification de la mise en œuvre des différentes étapes.

#### Visitor (Visiteur)
Le modèle de visiteur est utilisé pour séparer un ensemble relativement complexe de classes de données structurées de la fonctionnalité qui peut être exécutée sur les données que l'on veut traiter.

[Source](http://www.blackwasp.co.uk/gofpatterns.aspx)

### Astuces

* [les tableaux](/array.md)

## Conventions et bonnes pratiques

* [Le guide Ruby](/Ruby/ruby-style-guide.md) [³](#source-3)
* [Le guide Ruby on Rails](/Ruby/rails-style-guide.md) [⁴](#source-4)
* [Le guide de Bonne Pratiques](/Ruby/bonnes-pratiques.md) [⁵](#source-5)
* [Le guide de Bonne Pratiques Css](/Css/bonnes-pratiques-css.md) [⁶](#source-6)

*<a name="source-3">³</a>: D'après [porecreat](https://github.com/porecreat/ruby-style-guide/blob/master/README-frFR.md)*\
*<a name="source-4">⁴</a>: D'après [bbatsov](https://github.com/bbatsov/rails-style-guide)*\
*<a name="source-5">⁵</a>: D'après [Elevated Abstractions](http://elevatedabstractions.wordpress.com/2013/07/20/why-i-avoid-private-methods/) via [Elevated Abstractions](http://elevatedabstractions.wordpress.com/2013/07/20/why-i-avoid-private-methods/)*\
*<a name="source-6">⁶</a>: D'après [csswizardry](https://github.com/csswizardry/CSS-Guidelines)*
