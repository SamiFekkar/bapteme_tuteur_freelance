# Atelier Solo : Triple Triad Deck Builder

## Commentaire :

Tout d'abord, félicitations à toi, car dans l'ensemble, tu as bien réalisé cet atelier solo. Tu as compris les principes pour communiquer avec la base de données et les interactions entre les différents éléments : DataMapper, Controller, View, Router.

Il y a quand même un point sur lequel tu devrais faire attention :
### L'injection SQL :
Voici la requête que tu as utilisée dans le DataMapper :
```
const selectQuery = 
    `
    SELECT *
    FROM "card"
    WHERE "id" = ${id}
    `
;
```
Ici, tu utilises la valeur de la variable __id__ directement dans la requête SQL. Si une personne malveillante parvient à insérer une chaîne de caractères dans la valeur de __id__, cela peut compromettre la requête et permettre d'accéder à des données confidentielles de la base de données.

Crée plutôt ta requête de cette façon :
```
const selectQuery = {
  text: 'SELECT * FROM "card" WHERE "id" = $1',
  values: [id],
};
```
Ici, j'ai utilisé la syntaxe __$1__ pour représenter la valeur de l'identifiant (id) et j'utilise __values: [id]__, qui sert à lier cette valeur au paramètre $1 de la requête.  
Lorsque cette requête est envoyée à la base de données, le serveur SQL sait qu'il doit traiter le paramètre $1 en tant que valeur distincte plutôt que de le concaténer directement dans la requête SQL. De cette manière, la base de données est protégée contre les attaques d'injection SQL.

Lorsque tu fais appel à ton DataMapper depuis ton Controller, comme ici par exemple :
_CardsController.js_ : 
```
item: async (req, res) => {
    const id = Number(req.params.id);
    try {
      const card = await dataMapper.getOneCard(id);
      res.render('card', { card });
    } catch (error) {
      console.error(error);
      res.status(500).send(`An error occurred with the database :\n${error.message}`);
    }
  }
```
Pense à vérifier le retour afin de vérifier si l'élément existe bien. Ainsi, s'il n'existe pas, tu peux gérer cette erreur. Tu trouveras un exemple dans la correction de l'atelier dans le fichier _mainController.js_ dans la méthode _cardDetails_.

Lorsqu'on ajoute une carte dans le deck, tu as bien pensé à vérifier si la carte existe déjà avec le _find_ 👌.  
Une petite condition supplémentaire pour vérifier la longueur du tableau _deck_ et tu cochais toutes les cases 🫡

N'hésite pas à continuer tranquillement l'atelier en corrigeant tes erreurs et en tentant les bonus (Il n'y a rien que tu ne sais déjà faire).