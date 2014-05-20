#Les méthodes privées

*Les schémas sur les [slides](http://fr.slideshare.net/mercury_wood/amliorer-la-qualit-du-code-par-restriction-du-langage) peuvent aider à comprendre*

Prenons le cas d’utilisation des méthodes privées. Nous avons une classe avec une méthode publique est trop imposante et nous souhaitons la découper en plusieurs morceaux. Pour cela, nous créons deux méthodes privées, que la méthode publique appellent l’une après l’autre et nous partageons le code entre les deux. Il semblerait que nous avons gagné en lisibilité puisque nous avons des unités de code plus petites et nous avons pu nommer deux nouveau morceaux de code. Il subsiste cependant des problèmes majeurs.


**Problèmes**

* Le code du test est resté le même. Pourtant, si la méthode testée était imposante, alors le test est sûrement lui aussi imposant, et il l’est toujours ! Nous n’avons donc rien gagné en termes de modularité. Le gain est strictement visuel.
* Il est possible qu’une ou plusieurs des méthodes privées n’accèdent à aucun champ de la classe. De toute évidence elle n’a rien à faire dedans.
* Une méthode privée a toutes les libertés au sein d’une classe. Lorsqu’une méthode privée est appelée, il est impossible de savoir quels peuvent être ces effets sur les champs environnants, tout comme si l’on avait à faire a des variables globales. Ceci diminue la lisibilité.
* Elles n’aident aucunement à encapsuler, contrairement à certaines croyances (voir l’alternative).
* Elles peuvent sournoisement cacher des concepts importants (voir l’alternative).


**Alternative**

Une solution bien meilleure consiste à exporter les méthodes privées vers de nouvelles classes, où elles sont publiques. La ou les nouvelles classes deviennent alors des dépendances de la classe d’origine (des objets de type correspondant lui sont passés par son contructeur).

* Le test peut alors mocker ces dépendances et se contenter de tester la méthode d’origine, et elle seule (il est bien évidemment nécessaire d’écrire de nouveaux tests pour les nouvelles classes et méthodes).
* Chaque méthode n’a accès qu’à ce qui lui est nécessaire, et rien d’autre.
* Le développeur sera forcer de trouver un nom pour la ou les nouvelles classes, ce qui lui permettra de découvrir de nouveaux concepts, potentiellement importants, de son domaine métier. Par ailleurs, si ce concept est amené à évoluer par demande client, alors les modifications seront hermétiquement encapsulées par la classe qui l’implémente.
* La dépendance entre la classe d’origine et les nouvelles est implémentée au travers d’un champ privé. Il n’est toujours pas possible d’accéder aux méthodes anciennement privées lorsque l’on a un objet du type de la classe d’origine.
Article de ce blog sur le sujet : Why I Avoid Private Methods
