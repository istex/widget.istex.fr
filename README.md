# widget.istex.fr

Widgets ISTEX (search, results, facets) permettant de créer rapidement des interface Web d'interrogation des ressources ISTEX.

[![Build Status](https://travis-ci.org/istex/widget.istex.fr.svg?branch=master)](https://travis-ci.org/istex/widget.istex.fr)

## Usage classique des widgets

Exemple d'utilisation classique des widgets search et results. Il est nécessaire dans un premier temps de charger les fichiers JS et CSS des widgets Istex (head de la page HTML) ainsi que la librairie jQuery qui est une dépendance nécessaire.

Ensuite vous pouvez placer  deux éléments (zone de recherche & zone de résultats) où vous le souhaitez dans votre page HTML.
Finalement il reste à exécuter les deux plugins (un par widget) sur ces deux éléments.

Voici ce que ca peut donner sur une page quasi vierge :

```html
<html>
  <head>
    
    <!-- jQuery est une dépendance nécessaire -->
    <script src="//code.jquery.com/jquery-1.11.1.min.js"></script>
    
    <!-- Charge les widgets Istex -->
    <script type="text/javascript" src="//istex.github.io/js/widgets.min.js"></script>
    <link rel="stylesheet" href="//istex.github.io/themes/default/widgets.min.css" />

    <style>
      #istex-widget-search, #istex-widget-results {
          width: 600px;
      }
    </style>

  </head>
  <body>

    <div id="istex-widget-search"></div>
    <script type="text/javascript">
        $('#istex-widget-search').istexSearch();
    </script>

    <div id="istex-widget-results"></div>
    <script type="text/javascript">
        $('#istex-widget-results').istexResults();
    </script>

  </body>
</html>
```

## Paramètres des widgets

Les paramètres suivants peuvent être positionnés :

```javascript
var istexConfig = {
  // l'adresse de l'API de l'Istex
  istexApi: 'https://api.istex.fr',
  
  // pour lancer une recherche au chargement de la page
  // positionner les mots à rechercher
  query: "",
  
  // le nom de l'évènement émit au moment d'une recherche    
  resultsEventName: "istex-results",

  // la taille max en nombre de caractères du résumé
  abstractLength: 250,

  // la taille max en nombre de caractères du titre
  titleLength: 100,

  // quel est le format clickable au niveau du titre
  fullTextOnTitle: 'pdf'
};
```


## Fonctionnement du widget istexSearch

Ce widget permet d'insérer dans la page HTML une zone de saisie ainsi qu'un bouton de recherche. Lorsqu'une suite de mots sont tapés puis que le bouton rechercher est pressé, l'API Istex est interrogée à travers des requêtes AJAX. Une fois les résultats reçus, ils sont propagés aux widgets results et facets mais également à l'ensemble du DOM sous la forme d'un événement javascript (par défaut nommé "istex-results").

## Fonctionnement du widget istexResults

Ce widget permet d'insérer dans la page HTML la liste des résultats issus d'une recherche. Il a besoin donc besoin du widget istexSearch pour fonctionner. En effet, il se charge de capturer l'évènement "istex-results" puis de construire la liste des résultats à l'endroit souhaité dans la page HTML.

## Documentation développeurs

### Installation d'un environnement de développement

Voici les étapes permettant de mettre en place une environnement de développement :

Installer NodeJS et npm (exemple sous Linux avec l'outil [nvm](https://github.com/creationix/nvm)) :
```
curl https://raw.githubusercontent.com/creationix/nvm/v0.20.0/install.sh | bash
nvm install 0.10
nvm use 0.10
```

Récupérer le dépôt git des widgets Istex :
```
git clone git@github.com:istex/widget.istex.fr.git
```

Initialiser les dépendances (gulp est l'outil de build) :
```
cd widget.istex.fr/
npm install
npm install -g gulp
gulp init
```

Vous êtes alors opérationels pour développer votre contribution.

### Tester, compiler et déployer

Pour développer et tester les widgets depuis votre navigateur Web, le plus simple est de lancer un mini serveur Web avec la commande suivante :
```
gulp http
```
Puis ouvrez les URL qui s'affichent dans votre navigateur. Exemple: http://127.0.0.1:8080/index.html pour une vue d'ensemble.

Les tests unitaires se trouvent dans le répertoire ''./test/'' (le [framework mocha](http://mochajs.org/) est utilisé), pour les exécuter, tapez :
```
gulp test
```

Pour compiler les widgets vers le répertoire ''./dist/'', tapez :
```
gulp build
```
Pour déployer les widgets sur le site [istex.github.io](http://istex.github.io/) ([dépôt git](https://github.com/istex/istex.github.io)), tapez :
```
gulp deploy
```
