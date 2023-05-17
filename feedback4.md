# Atelier Solo : Triple Triad Deck Builder

## Commentaire :

Tu as su créer la méthode getCard dans le dataMapper, ainsi que la requête SQL, cependant tu as oublié d'utiliser le paramètre __id__ dans ta requête afin de la dynamiser.
La requête ne sait donc pas à quoi correspond le __$1__ : 
```
const queryResult = await client.query(
`SELECT * 
FROM card 
WHERE card.id = $1;
`);
```
Voici un exemple de comment utiliser le paramètre dans la requête SQL :
```
const selectQuery = {
  text: 'SELECT * FROM "card" WHERE "id" = $1',
  values: [id],
};
```
Ici, j'ai utilisé la syntaxe __$1__ pour représenter la valeur de l'identifiant (id) et j'utilise __values: [id]__, qui sert à lier cette valeur au paramètre __$1__ de la requête. 
Cela me permet également de protéger ma requête d'éventuelle injection SQL.

Dans le _mainController.js_, tu as bien importé le dataMapper et tu as bien créé la méthode _cardPage_ utilisant la _getCard_ du dataMapper, puis appelé la view _card_. Malheureusement, tu ne passes pas le résultat de _getCard_ à ta view, il est donc impossible d'utiliser cette valeur dans la view.

Tu as bien créé la nouvelle route dans le _router.js_, mais celle-ci n'est pas dynamique. Je te mets un exemple pour rendre cette route dynamique et ainsi pouvoir utiliser dans le _dataMapper_ le `request.params.id` :
```
router.get('/card/:id', mainController.cardPage);
```
Pour que cette route soit utilisée, il faut mettre à jour les liens (href) dans la view de la page d'accueil.

## Conclusion :
Tu as su écrire la requête SQL, il restait à la dynamiser. Tu as également su écrire les méthodes du _dataMapper.js_ et du _mainController.js_. Pense à vérifier que tu utilises bien les paramètres de tes méthodes. 
Je te conseille de reprendre depuis le début en prenant ton temps pour ne rien oublier. Avant de recommencer cet atelier, n'hésite pas à revoir quelques notions :
* Dynamiser une route.
* Récupérer les `request.params`.
* Comment passer une variable à une view ejs et comment l'utiliser depuis la view.

S'il y a des notions que tu n'as pas comprises, n'hésite pas à venir me voir sur Slack.