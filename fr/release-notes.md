---
layout: fr
title: Notes de versions
id: release-notes
---

# {{ page.title }}

## 2.3.12 *15 décembre 2015*

- __compilateur__
  - Correction de problèmes sur IE 9/10 et autres bugs mineurs
  - Ajout de l'option `exclude` pour supprimer des portions de vos tags en sortie comme `css`, `js` ou `html`
  - Ajout de `url` comme troisième argument de la méthode `compile` pour un meilleur débogage en sortie
- __route__
  - Corrections de problèmes importants sur IE et Safari
  - Correction d'une [régression API](https://github.com/riot/route/issues/30)
- __riot-cli__
  - Ajout de l'option `--config` pour charger vos options CLI et vos parseurs depuis un fichier de configuration ES6 externe [plus de détails](/fr/guide/compiler/#es6-config-file)
  - Ajout d'un meilleur support de `babel 6` si combiné avec notre preset [babel-preset-es2015-riot](https://github.com/riot/babel-preset-es2015-riot)
- __riot__
  - Ajout de la transclusion multiple [plus de détails](/fr/api/#multi-transclusion)
  - Correction des boucles contenant des éléments `null`

## 2.3.11 *22 november 2015*

- __compilateur__
  - Suppression des restrictions sur l'indentation nulle pour les tags personnalisés, maintenant vous pouvez indenter ces tags, mais le tag d'ouverture et de fermeture doivent être au même niveau d'indentation (en longueur et en type). Toute l'indentation du tag sera retranchée de cette quantité.
  - Support des attributs `src` et `charset` dans les balises `<script>` pour lire des sources JavaScript depuis le système de fichiers - [riot#507](https://github.com/riot/riot/issues/507)
  - La fonction `compile` peut retourner des parties séparées en renseignant la nouvelle option `entities`. Ces parties ont des sauts de ligne non échappés.
  - Le nouvel attribut `options` pour les balises `script` et `style` viendra ajouter/écraser les attributs dans la configuration par défaut du parseur au niveau du tag.
  - Correction [riot#1261](https://github.com/riot/riot/issues/1261): la balise `<pre>` ne préserve ni `\n` ni `\t`.
    Maintenant les espaces dans les balises `<pre>` sont toujours préservés.
  - Correction [riot#1358](https://github.com/riot/riot/issues/1358): Un style scopé vide fait crasher.
  - Correction [riot#1306](https://github.com/riot/riot/issues/1306): Le compilateur préserve les sauts de ligne dans les classes, causant des erreurs "Unterminated String Constant".
  - Correction [riot#1314](https://github.com/riot/riot/issues/1314): `settings.brackets` ne fonctionnait plus.

- __riot__
  - Correction de `riot.render` sur les vieilles versions de Node
  - Correction de quelques petits bugs sur les boucles
  - Correction: `riot.route` ne bloque plus les liens non inscrits avec `event.preventDefault`
  - Ajout de l'événement `error` sur tous les instances `riot.observable` pour intercepter toutes les erreurs possibles déclenchées au sein des callbacks

- __riot-cli__
  - Ajout de meilleurs messages d'erreur si le parseur n'est pas installé localement
  - Ajout de l'option `export` pour extraire des portions de vos tags comme `css`, `js` ou `html`
  - Ajout de l'option `style` pour choisir le préprocesseur par défaut de vos balises de style
  - Ajout du support natif des préprocesseurs `sass`, `scss` et `less`

## 2.3.1 *10 novembre 2015*

- Ajout du parseur `babel` pour supporter babel 6 sorti tout récemment; utilisez `es6` si vous voulez toujours utiliser les versions précédentes de babel
- Ajout de `riot.route.start(autoExec)` qui démarre le routeur et exécute automatiquement la route associée à l'URL en cours.
- Suppression de `compiler.js` `compiler.min.js` dans le répertoire projet, utilisez toujours `riot+compiler.js` à la place
- Correction de [l'option `modular`](https://github.com/riot/cli/issues/7) dans `riot-cli`
- Correction de la méthode [`riot.render`](https://github.com/riot/riot/pull/1330)

## 2.3.0 *5 novembre 2015*

Cette nouvelle version majeure est un grand pas en avant pour Riot et fixe [de nombreux problèmes](https://github.com/riot/riot/issues?q=is%3Aissue+milestone%3A2.3.0+is%3Aclosed) en organisant le code dans plusieurs modules.
Riot a été divisé en 6 modules différents:

- [compiler](https://github.com/riot/compiler)
- [tmpl](https://github.com/riot/tmpl)
- [observable](https://github.com/riot/observable)
- [route](https://github.com/riot/route)
- [core](https://github.com/riot/riot)
- [cli](https://github.com/riot/cli)

Voici la liste des plus gros changements:

- Ajout de l'API History de HTML5 au routeur, veuillez consulter la [documentation](/api/route/)
- Versions réécrites du compilateur, du moteur de templates et de l'interface en ligne de commandes
- Dépréciation de `riot.mountTo`
- Changement de `tag._id` en `tag._riot_id` **vous ne devriez pas utiliser les propriétés internes de Riot de toute façon**
- Correction de `yield` côté serveur
- Correction d'une fuite mémoire dans `riot.render`
- Correction des attributs dynamiques tels que `name` `id`
- Nouveau comportement pour les boucles, elles sont un peu plus lentes mais plus fiables ; vous pouvez utiliser l'option `no-reorder` si vous voulez utiliser l'algorithme précédent plus rapide ([plus de détails ici](/guide/#loops-advanced-tips))


## 2.2.4 *12 août 2015*

- Correction des bugs restants du noyau avant la plus grosse livraison 2.3.0 ; [plus de détails](https://github.com/riot/riot/issues?q=is%3Aissue+milestone%3A2.2.4)
- Support de multiples blocs de styles au sein du même composant
- Correction de bugs liés à la perte du contexte dans les boucles imbriquées
- Ajout de plus de tests dans la base de code
- *NOTE*: ceci est la dernière version stable avant l'abandon du support IE8
- [Roadmap à court terme](https://github.com/riot/riot/issues/1063)

## 2.2.3 *4 août 2015*

- Correction de nombreux bugs ; [plus de détails](https://github.com/riot/riot/issues/1063)

## 2.2.2 *5 juillet 2015*

- Nouveau: les composants enfants héritent des propriétés de leur parent, y-compris dans une boucle
- Nouveau: riot est capable de compiler les attributs sur le tag de plus haut niveau ; [plus de détails](https://github.com/riot/riot/issues/948)
- Amélioration de la performance des boucles et nombreux correctifs de bugs
- Amélioration de la compatibilité AMD/CommonJS
- Correction de l'erreur renvoyée dans le compilateur pour les tags utilisant l'attribut `type=text/javascript`
- Correction des variables du parent qui n'était pas exposées aux enfants dans une boucle, maintenant __tous les enfants dans une boucle héritent des propriétés et méthodes de leur parent__ ; [plus de détails](https://github.com/riot/riot/issues/896)
- Correction de l'erreur renvoyée lorsque l'on essayait de surcharger des propriétés d'évènements en lecture seule
- Correction de riot cli combiné au flag --modular quand il n'y a pas de fichier de destination spécifié

## 2.2.1 *28 juin 2015*

- Correction des options qui étaient mal passées aux enfants dans une boucle ; [plus de détails ici](https://github.com/riot/riot/issues/884)

## 2.2.0 *27 juin 2015*

- Nouvelle logique super rapide pour les boucles (les noeuds DOM ne seront plus réordonnés, [plus de détails ici](https://github.com/riot/riot/issues/484))
- Autorise à nouveau le mode `use strict`
- Autorise à nouveau le mode `coffescript` pour les nostalgiques
- Inconsistances réglées lorsque l'on utilisait des boucles avec des listes vides ou nulles
- Correction de `mount` dans les éléments enfants des boucles
- Couverture de code augmentée
- Ajout de la possibilité de spécifier où riot doit injecter le [CSS des tags personnalisés](/guide/#scoped-css) dans le DOM

La liste des correctifs de bugs et les détails peuvent être trouvés [ici](https://github.com/riot/riot/issues/773)

## 2.1.0 *20 mai 2015*

- [Mixins](/guide/#mixins)
- Possibilité de définir des attributs sur l'élément racine de la définition du tag
- Séparation du compilateur node et du compilateur sur navigateur
- Script de build simplifié avec [smash](https://github.com/mbostock/smash)
- Ajout des branchements Saucelabs pour les tests multi-navigateurs
- Ajout des branchements Coveralls pour vérifier la couverture de code à chaque pull request

La liste des correctifs de bugs et les détails peuvent être trouvés [ici](https://github.com/riot/riot/issues/648)

## 2.0.15 *23 avril 2015*

- Le nouveau tag central `<yield>` permet la [transclusion HTML](/guide/#nested-html)
- Un nouvel attribut [riot-tag](/guide/#html-elements-as-tags) pour utiliser des éléments HTML standards comme points de montage
- Ajout de `tag.unmount(flag)` pour décider si le parent doit être supprimé ou non du DOM
- Ajout des méthodes `riot.route.start()` et `riot.route.stop()` pour démarrer et arrêter le routeur Riot. Ces méthodes vous permettent d'utiliser un routeur différent pour votre application.
- Le compilateur côté serveur supporte maintenant les modules AMD et CommonJS avec l'option de ligne de commande `--modular` ou `-m`
- Nombreux [correctifs de bugs](https://github.com/riot/riot/issues/584)
- Remerciements particuliers à *[@GianlucaGuarini](https://github.com/GianlucaGuarini)* pour cette livraison


## 2.0.14 *8 avril 2015*

- [Rendu côté serveur](/guide/#server-side-rendering)
- [Corrections de bugs](https://github.com/riot/riot/compare/v2.0.13...v2.0.14)

## 2.0.13 *11 mars 2015*

- Une grosse livraison de correctifs de bugs consistuée uniquement de [pull requests](https://github.com/riot/riot/compare/v2.0.12...v2.0.13) de la part de la communauté. Merci à vous !
- [Suite de tests](https://github.com/riot/riot/tree/master/test) plus importante

## 2.0.12 *2 mars 2015*

- Support des [Scopes CSS](/guide/#scoped-css)
- Accès direct aux [tags imbriqués](/api/#nested-tags) et à leur API via la variable `tags`. Par exemple: `tags.my_timer.clear()`
- Les tags personnalisés sont maintenant construites pendant la phase de lecture et initialisées pendant la phase de montage. Ceci est un travail préliminaire pour le prochain [système de plugins](https://github.com/riot/riot/issues/416) et permet aux plugins de faire leur boulot avant l'initialisation.
- L'option `--whitespace` du compilateur préserve les nouvelles lignes et espaces blancs dans le code généré. Bien pour les éléments imbriqués `pre` et `textarea`.
- Utilisation de [Karma](http://karma-runner.github.io/0.12/index.html) pour le test multi-navigateurs.
- *ATTENTION* le déprécié `riot.mountTo` sera supprimé à la prochaine livraison


## 2.0.11 *23 février 2015*

- `riot.mount` accepte maintenant les mêmes paramètres que `riot.mountTo`, qui est maintenant *deprécié*
- Le nouveau `riot.mount(selector, tagName, opts)` vous permet de monter un certain tag sur n'importe quelle sélection d'éléments HTML
- `riot.unmount` suivi par `riot.mount` remplace maintenant correctement le tag précédent
- Suite de tests v1. Attendez-vous à la voir grandir en taille et en fonctionnalités. Merci à [@GianlucaGuarini](https://github.com/GianlucaGuarini)


## 2.0.10 *19 février 2015*

- [Exemple Todo MVC](https://github.com/txchen/feplay/tree/gh-pages/riot_todo)
- Les éléments de liste peuvent être triés et arrangés et la vue se mettra à jour en fonction. Merci à [@pakastin](https://github.com/pakastin)!
- Les balises `style` imbriquées sont automatiquement injectées dans `<head>` pour éviter un duplicat des definitions
- Possibilité de définir des tags sur la même ligne: `<tag></tag>`
- Support de la notation en une ligne pour les méthodes ES6: `foo() { this.bar = 'baz' }`
- Pas de requêtes serveur illégales avec les images: `<img src={ src }>`
- Correction du compilateur pour supporter les notations crochets personnalisées
- `this.update()` n'est plus nécessaire pour définir des tags manuellement avec `riot.tag`. Cette méthode est maintenant automatiquement appelée après qu'un gestionnaire d'évènements est exécuté
- [Guidelines pour les contributeurs](https://github.com/riot/riot/blob/master/CONTRIBUTING.md)


## 2.0.9 *13 février 2015*

- Support de LiveScript
- Possibilité de définir les attributs `if`, `show` et `hide` pour un tag personnalisé
- Raccourci pour les classes multiples: `{ 'foo bar': baz }`
- Propriété `children` retirée, son besoin était surtout théorique.
- Fuite mémoire corrigée sur `riot.observable`. Merci à [@GianlucaGuarini](https://github.com/GianlucaGuarini) pour le gros travail de débogage et à tous les autres sur cette [pull request](https://github.com/riot/riot/issues/248)


## 2.0.8 *9 février 2015*

- Nouvelle méthode `unmount()` et nouvelle propriété `children[]` pour les [instances de tags](/api/#tag-instance)
- Flux de données mono-directionnel: les mises à jour et démontages se propagent toujours vers le bas du parent aux enfants
- L'attribut `if` fonctionne maintenant comme prévu en ajoutant ou supprimant le noeud racine du DOM
- [L'API du compilateur](/api/compiler/) est désormais exposée au public
- Les variables globales sont supportées dans les expressions, i.e. `{ location }`
- Extension `.tag` personnalisable, i.e. `riot --ext html`
- [Notation crochets](/api/misc/#brackets) personnalisable, i.e. `riot.settings.brackets = '${ }'`
- Possibilité d'afficher la version actuelle avec: `riot --version`
- La fonction à moitié cachée `riot._tmpl()` est désormais complètement cachée et ne fait plus partie de l'objet global `riot`
- Code source réorganisé. L'ancien gros `view.js` est désormais divisé en [multiples fichiers](https://github.com/riot/riot/tree/master/lib/browser/tag)


## 2.0.7 *29 janvier 2015*

- [Compilation dans le navigateur](/guide/compile/) super rapide pour: `<script type="riot/tag">`
- [Support natif de Typescript](/guide/compiler/#typescript)
- Possibilité de brancher un préprocesseur HTML (aux côtés d'un préprocesseur JS)
- Support natif de [Jade](/guide/compiler/#jade)
- Possibilité de définir des [interpréteurs personnalisés](/api/#route-parser) pour le routeur
- Les balises peuvent être du XML valide et les balises vides HTML5 ne sont pas auto-fermantes
- Autorise la définition de tags vides pour réserver un espace. Bien pour la phase de développement.
- `riot.observable()` retourne maintenant un nouvel observable quand il est appelé sans argument
- Le compilateur s'appelle désormais comme ceci:


```
var riot = require('riot')
var js_string = riot.compile(tag_source_string)
```


## 2.0.5 *27 janvier 2015*

- Possibilité de brancher un préprocesseur JavaScript
- Support natif de CoffeeScript
- Support natif de EcmaScript 6


## 2.0.2 *26 janvier 2015*

- Support de CommonJS et AMD
- Support de Component
- Support de Bower
- `npm install` fonctionne maintenant avec io.js et node 0.11
- `require('riot')` retourne maintenant riot.js (pour bien s'accorder avec Browserify etc.)
- `require('riot/compiler')` retourne le compilateur
- `riot.js` et `riot.min.js` se trouvent maintenant à la racine du répertoire
- hébergé sur [cdnjs](https://cdnjs.com/libraries/riot) et [jsdelivr](http://www.jsdelivr.com/#!riot)


## 2.0 *22 janvier 2015*

[A React- like, 2.5KB user interface library](https://muut.com/blog/technology/riot-2.0/)

Une mise à jour significative et non rétrocompatible.

![](https://muut.com/blog/technology/riot-2.0/riot1to2.png)


## 1.0 *15 avril 2014*

Suppression de jQuery en dépendance.


## 0.9 *1er Novembre 2013*

[The 1kb client-side MVP library](https://muut.com/blog/technology/riotjs-the-1kb-mvp-framework.html)

Version initiale.
