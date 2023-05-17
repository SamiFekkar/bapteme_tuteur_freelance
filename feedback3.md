# Atelier Solo : Triple Triad Deck Builder

## Commentaire :

## Étape 1 : Détail d'une carte

Tu as bien réussi les premières étapes, ce qui montre que tu as compris comment fonctionnait l'application et les liens qu'il y avait entre les différents éléments : DataMapper, Controller, View, Router.
Tu as bien fait attention à l'injection SQL lors de ta requête.

Je pense que tu t'es embrouillé avec l'EJS. Sur la view de détails d'une carte, pas besoin de boucler sur un tableau de cartes, car la variable que tu passes à ta view est l'objet __oneCard__ et non pas un tableau de cartes. La boucle _for of_ n'a pas lieu d'être :
_views/main/cardDetails.ejs_
```
<% for (const singleCard of card) { %>
```
D'ailleurs, le nom de la variable que tu passes à ta view est __oneCard__, et non __card__. Ta view ne connaît donc pas cette variable.

Tu pourras regarder la correction pour t'inspirer du code EJS dans la view: _views/cardDetails.ejs_.

Dernière petite remarque concernant l'EJS, sur la boucle _for of_, j'ai l'impression que tu as inversé la variable sur laquelle tu veux boucler et celle que tu utilises une fois dans la boucle.
Même si tu n'avais pas besoin de boucle ici, je te mets un exemple d'une boucle _for of_ fonctionnelle comme rappel :

Ici, on boucle sur le tableau __cards__, et chaque objet de ce tableau sera utilisé via la variable __card__, donc __card.name__, __card.id__, etc.
```
  <% for (const card of cards) { %> 
    <div class="card">
      <a href="/card/<%= card.id %>">
        <img src="/visuals/<%= card.visual_name %>" alt="<%= card.name %> illustration">
        <p class="cardName"><%= card.name %></p>
      </a>
      <a class="link--addCard" title="Ajouter au deck" href="/deck/add/<%= card.id %>">[ + ]</a>
      <a class="link--removeCard" title="Supprimer du deck" href="/deck/remove/<%=card.id %>">[ - ]</a>
    </div>

  <% } %>
```

## Étape 2 : Recherche

Malgré le fait que ta view ne fonctionne pas, tu n'as pas pour autant abandonné et tu as continué cet atelier 💪.  
Tu as bien écrit ta requête et ta méthode dans le dataMapper ainsi que dans le controller, tu as bien créé la view et fait le routing dans le router.  
Ça montre que tu as compris les étapes.  
Cependant, certaines erreurs empêchent le bon fonctionnement de l'application :
* Dans le searchController.js, tu as oublié d'importer ton dataMapper, il est donc impossible d'utiliser la méthode : _dataMapper.cardElement(element)_. Le nom de la méthode appelée n'est pas le bon également, car dans ton dataMapper tu l'as appelé : _getCardByElement_.
* Lorsque tu appelles la méthode cardElement, tu lui passes bien l'__element__, cependant tu as récupéré cet élément via : `request.params.element`. L'utilisation de `request.query.element` te permet de récupérer la bonne valeur car `request.query.element` permet de récupérer les variables de l'URL pour un élément : element?element=terre.
* Dans le _dataMapper_, tu n'utilises pas le paramètre __element__ que tu lui as passé, la query n'est donc pas dynamique et elle récupère tous les éléments qui ne sont pas _NULL_.


## Conclusion :
Comme je l'ai déjà dit plus haut, tu as compris comment communiquer depuis la base de données jusqu'à la view.
Certaines erreurs d'import, de nom de variable/méthode etc. t'empêchaient d'avoir un rendu sur le navigateur.
Avec la correction, essaie de corriger tes erreurs et ensuite je pense que tu peux continuer là où tu t'étais arrêté et finir cet atelier.