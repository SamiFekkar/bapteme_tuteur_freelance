Donc, si j'ai bien compris, tu aimerais en savoir plus sur Fetch :

Fetch est une fonction JavaScript qui permet d'envoyer des requêtes HTTP depuis un navigateur web. Les requêtes HTTP sont des demandes envoyées par le navigateur à un serveur web pour obtenir des informations (GET) ou pour envoyer des informations au serveur (POST, PUT, DELETE). Par exemple, dans le cas du parcours Triple Triad, le serveur que tu as crée permet d'obtenir la liste des cartes etc.

En utilisant la méthode Fetch, on peut faire une requête à ton serveur depuis le navigateur pour récupérer les informations demandées, comme la liste des cartes ou une carte particulière en fonction de la route utilisée. Lorsque ton serveur tourne en local, il est accessible depuis l'URL de ton localhost, par exemple http://localhost:1234.

Voici un exemple d'utilisation de Fetch pour récupérer une carte particulière en utilisant son ID (par défaut, Fetch utilise la méthode GET) :

```
async function fetchData() {
  try {
    const response = await fetch('http://localhost:1234/card/1');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

fetchData();
```

Ici, on appelle le serveur en utilisant l'adresse de ton localhost pour récupérer une seule carte en utilisant son ID. Le serveur est censé renvoyer les informations récupérées dans la base de données.

Si l'on veut ajouter une carte à notre base de données, on utilisera la méthode POST :

```
async function addNewCard(cardData) {
  try {
    // on utilise la méthode fetch pour envoyer une requête POST
    const response = await fetch('http://localhost:1234/card', {
      method: 'POST', // méthode HTTP utilisée
      headers: {
        'Content-Type': 'application/json' // format de données envoyées
      },
      body: JSON.stringify(cardData) // les données à envoyer, converties en format JSON
    });
    const data = await response.json(); // on attend la réponse, qui est également en format JSON
    console.log(data); // on affiche la réponse dans la console
  } catch (error) {
    console.error(error); // en cas d'erreur, on affiche l'erreur dans la console
  }
}

// on appelle la fonction addNewCard avec les données de la nouvelle carte à ajouter
addNewCard({
  name: 'Nouvelle carte',
  strength: 7,
  element: 'Feu'
});
```

Dans cet exemple, nous utilisons la méthode fetch pour envoyer une requête POST avec les données d'une nouvelle carte. Les données sont envoyées en format JSON et le serveur est censé les stocker dans la base de données. Ensuite, nous affichons la réponse dans la console pour vérifier que l'opération a réussi.
