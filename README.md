ruby-conventions
================

Ruby conventions and style guide in French

## Règles pour Ruby et Ruby on Rails

D'apres [Sandi Metz'](http://rubyrogues.com/087-rr-book-clubpractical-object-oriented-design-in-ruby-with-sandi-metz/) :

  1. Une classe ne doit pas dépasser **100 lignes** de code.
  2. Une méthode ne doit pas dépasser **5 lignes** de code.
  3. Une méthode ne doit pas avoir plus de **4 paramètres**.[^1]
  4. Un controlleur doit instancier **1 seul objet**.[^2]

[^1]: Hash comprit
[^2]: Utiliser le pattern **Facade** ou **Présenteur**


## Règles pour Ruby on Rails

D'après [Guirec Corbel](http://gcorbel.github.io/blog/blog/2013/10/12/quand-jutilise-des-helpers-des-partials-des-presenters-et-des-decorators/) :

###Les Helpers

Les Helpers sont des méthodes génériques qui peuvent être utilisées pour différents types d’objet. On peut créer des helpers du style ```link_to_update```, ```big_image```, ```styled_form```, etc. Ces méthodes créent du code html avec, par exemple, un style css ou un texte standard.

###Les Partials

Les Partials sont utilisés pour diviser une grosse vue dans de plus petites parties logiques. On peut avoir un partial ```side_menu```, ```comment_list```, ```header```, etc.

###Les Presenters

Les Presenters sont créés pour des requêtes plus compliquées avec un modèle ou plus. On peut avoir des presenters comme ```@page_presenter.page_in_category(ruby_category)``` ou ```@user_presenter.user_following(an_article)```.

###Les Decorators

Les Decorators doivent interagir avec un seul modèle et ne doivent pas avoir de paramètres(si possible). On peut codder : ```user.full_name```, ```page.big_title``` ou ```category.permalink```. Utilisez la gem [Draper](https://github.com/drapergem/draper).

Si on utilise plusieurs modèles, on ne doit pas accéder à la classe du modèle directement dans la vue. Il est préférable d'utiliser la fonction de Draper [decorates_finders](https://github.com/drapergem/draper#decorated-finders).

## Conventions et bonnes pratiques

* [Le guide Ruby](/ruby-style-guide.md)
* [Le guide Ruby on Rails](/rails-style-guide.md)



