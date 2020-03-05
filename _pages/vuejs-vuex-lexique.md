---
ID: 460
post_title: VueJS / VueX Lexique
author: Epistol
post_excerpt: ""
layout: page
permalink: https://epistol.fr/vuejs-vuex-lexique/
published: true
post_date: 2019-10-10 12:49:40
---
<!-- wp:paragraph -->
<p><strong>Vue</strong> : est un&nbsp;<strong>framework évolutif</strong>&nbsp;pour construire des interfaces utilisateur</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Ecmascript 2015</strong> : largest addition to the JavaScript language </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>let</strong> : déclaration de variable dans un scope ( entre deux {} )</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"js"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="js" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">function test(){
  if( 1 === 1 ){
    let maVar = true;
    console.log(maVar);
    // Retourne true
  }
console.log(maVar);
  // Retourne une erreur, let n'existe pas hors du bloc "if"
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph {"align":"left"} -->
<p style="text-align:left"><strong>var</strong> : déclaration de variable à portée de fonction (accessible dans toute la fonction)</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"js"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="js" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">function test(){
  maVar = 'valeur';
}
test();
console.log(maVar);
// Retourne 'valeur'
console.log(window.maVar);
// Retourne 'valeur'</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p><strong>scope</strong> : portée d'une donnée, variable locale / globale (cf plus haut)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Cycle de fonctionnement de VueJS : </p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":464,"align":"center"} -->
<div class="wp-block-image"><figure class="aligncenter"><img src="https://epistol.fr/wp-content/uploads/2019/10/3-404x1024.png" alt="" class="wp-image-464"/></figure></div>
<!-- /wp:image -->

<!-- wp:heading -->
<h2>VueX </h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
<h4>Adaptabilité et VueX</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Il s’agit d’un système de gestion d’état, non il ne s’agit pas de politique&nbsp;! Il s’agit de la gestion d’états de variables.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>La gestion des états permet entre autres de définir la portée des variables afin de&nbsp;<strong>séparer</strong>&nbsp;ce qui doit être accessible dans toute l’application de ce qui ne doit être accessible&nbsp;<strong>uniquement</strong>&nbsp;au sein d’un composant mais l’utilité principale de la gestion des états est de permettre de séparer la logique au sein d’une application afin d’assurer une meilleure&nbsp;<strong>structuration</strong>&nbsp;et&nbsp;<strong>maintenance</strong>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>L’exécution d’une application Vue basique se compose de 3 parties&nbsp;:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><strong>L’état</strong><ul><li>«&nbsp;Source de vérité&nbsp;», il s’agit principalement des données que l’on affectera aux variables que l’on utilisera</li></ul></li><li>La&nbsp;<strong>vue</strong><ul><li>Mapping déclaratif de l’état, nous allons nourrir notre DOM des données</li></ul></li><li>Les&nbsp;<strong>actions</strong><ul><li>Agissent sur l’état de nos données en fonctions du comportement de l’utilisateur. Un utilisateur peut déclencher un événement qui déclenchera à son tour une action à mener sur l’état.</li><li>Un changement d’état implique une mise à jour de la vévènementue.</li></ul></li></ul>
<!-- /wp:list -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://scr.sad.supinfo.com/articles/resources/216224/6959/4.png" alt=""/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Le problème de cette implémentation réside dans le fait que lorsque l’on veut développer une application de moyenne à très grande envergure, on peut se retrouver avec des composants qui se&nbsp;<strong>partagent</strong>&nbsp;un état ou des actions se trouvant dans des composants différents qui ont besoin de&nbsp;<strong>modifier</strong>&nbsp;un même état selon différents comportements.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>En&nbsp;<strong>passant des propriétés aux composants</strong>&nbsp;il est facilement possible de se partager un état avec Vue.&nbsp;<strong>Mais</strong>&nbsp;encore une fois en cas de très grosse application contenant de nombreux composants cela peut vite devenir ridiculement long particulièrement si on ajoute une propriété à se partager entre chaque composant.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Ensuite, dans le cas de la modification d’un état, il faudrait faire appel aux composants parents/enfants pour leur indiquer que celui-ci a été mis à jour et on se retrouve facilement avec un code presque impossible à maintenir avec de nombreuses actions qui font exactement la même chose.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Par exemple&nbsp;si j’ai deux plusieurs composants&nbsp;:&nbsp;<strong>panier</strong>&nbsp;et&nbsp;<strong>liste</strong>. Les produits qui seront affichés dans la&nbsp;<strong>liste</strong>&nbsp;proviennent d’un état. Si un utilisateur veut ajouter un produit à son panier, il serait dommage que le composant panier&nbsp;<strong>ne puisse pas communiquer</strong>&nbsp;avec mon état contenant la liste de produits dont le produit sélectionné.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>C’est pourquoi avec VueX, on mets à disposition une entité commune accessible de façon globale dans toute l’application permettant à n’importe quel composant d’effectuer actions, mutations sur un état.</p>
<!-- /wp:paragraph -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://scr.sad.supinfo.com/articles/resources/216224/6959/5.png" alt=""/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Pour faire simple, on distinguera nos fonctions en 3 catégories&nbsp;:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><strong>Mutateurs ou Setters</strong><ul><li>On utilisera cette fonction principalement lors de la mise à jour d’un état de variable.</li><li>Les mutateurs ne peuvent communiquer ni avec les actions ni avec les accesseurs. Ils ne servent qu’à mettre à jour une variable.</li><li>Sachez toutefois qu’il est possible de déclencher directement une mutation sans passer par une action.</li></ul></li><li><strong>Getters ou Accesseurs</strong><ul><li>On utilisera cette fonction principalement lorsque l’on voudra récupérer l’état d’une variable</li></ul></li><li><strong>Actions</strong><ul><li>Tout le reste</li></ul></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Selon un schéma bien défini, un utilisateur&nbsp;<strong>déclenche</strong>&nbsp;une action dans un composant qui va lui-même déclencher une&nbsp;<strong>action au sein de Vuex</strong>, l’action déclenchera la mutation d’un état.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Tous les composants utilisant un état détectent automatiquement les changements et mettent à jour la vue.</p>
<!-- /wp:paragraph -->

<!-- wp:image -->
<figure class="wp-block-image"><img src="https://scr.sad.supinfo.com/articles/resources/216224/6959/6.png" alt=""/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Ainsi, notre composant panier et liste peuvent tous les deux agir sur l’objet liste de façon très simple.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Les états des objets sont stockés dans ce que l’on pourrait appeler des «&nbsp;stores&nbsp;», pour accéder à ceux-ci il faudra alors&nbsp;<strong>obligatoirement</strong>&nbsp;passer par ces «&nbsp;stores&nbsp;», ceux-là sont immuables, il n’est donc pas possible de le modifier en dehors ce qui y a été déclaré. Il s’agit d’un fonctionnement analogue aux constantes on pourra dire.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li></li></ul>
<!-- /wp:list -->