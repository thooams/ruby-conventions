# Array

## Comment vérifier si un tableau contient tous les éléments d’un autre ?

Vérifier que tous les emails importés existent dans une liste de contact.

```ruby
imported_emails = [ 'john@doe.com', 'janet@doe.com' ]
existing_emails = [ 'john@doe.com', 'janet@doe.com' , 'fred@mercury.com' ]

puts 'already imported' if (imported_emails - existing_emails).empty?
```

Résultat IRB :

```
already imported
=> nil
```

Référence : [Array Difference](http://www.ruby-doc.org/core-2.1.0/Array.html#method-i-2D)

## Comment trouver quels éléments sont communs à deux tableaux ?

Trouver les tags communs entre deux articles de blog.

```ruby
tags_post1 = [ 'ruby', 'rails', 'test' ]
tags_post2 = [ 'test', 'rspec' ]

common_tags = tags_post1 & tags_post2
```

Résultat IRB :
```
=> ["test"]
```

Référence : [Set Intersection](http://www.ruby-doc.org/core-2.1.0/Array.html#method-i-26)


## Comment fusionner deux tableaux sans créer de doublon ?

Obtenir une liste unique d’ID de comptes Twitter suivis par deux personnes.

```ruby
followeds1 = [ 1, 2, 3 ]
followeds2 = [ 2, 4, 5 ]

all_followeds =  followeds1 | followeds2
```

Résultat IRB :
```
=> [1, 2, 3, 4, 5]
```
Référence : [Set Union](http://www.ruby-doc.org/core-2.1.0/Array.html#method-i-7C)

## Comment toujours récupérer un tableau ?

Dans une méthode on manipule des produits. A la fin de cette méthode on retourne un ou plusieurs produits.
Mais lorsque l'on n’en récupère un seul, celui-ci n'est pas un tableau.
On peut traiter les deux cas de manière très élégante avec Array() or [*]:

```ruby
def method
 # …

 [*products]
end
```

Référence : [Kernel#Array](http://www.ruby-doc.org/core-2.1.0/Kernel.html#method-i-Array), [splat operator](http://www.ruby-doc.org/core-2.1.0/doc/syntax/calling_methods_rdoc.html#label-Array+to+Arguments+Conversion)



*([source](http://blog.8thcolor.com/fr/2014/02/7-cas-d-usage-quotidien-d-un-tableau-en-ruby/))*
