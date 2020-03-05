---
ID: 47
post_title: 'L&rsquo;idée &#8211; Créer un thème (WP) en 2018 &#8211;  1/3'
author: lm437747
post_excerpt: ""
layout: post
permalink: >
  https://epistol.fr/article/creer-un-theme-wp-en-2018-1/
published: true
post_date: 2018-11-18 16:25:14
---
<!-- wp:paragraph -->
<p>Pour ce blog tout nouveau tout beau, il fallait que je recolle le thème au "personnal branding" Epistol, même si un peu délaissé depuis quelques temps, j'utilise le thème Lovecraft pour le moment qui fait un bon fallback pour l'instant.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Etape 1 : - Avoir une idée de thème</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Avoir une idée de thème, c'est comme celle d'avoir un blog, c'est pas la partie la plus simple.&nbsp; Que faire alors ? Plutôt horizontal ? Plutôt le contraire ? Sur un format 3/6/3 ? Ou un simple 3/9 ? Qu'est-ce que ça veut dire ?&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Si on veux créer le design d'un thème, on prend les références du marché actuel : <a href="https://getbootstrap.com/docs/4.1/layout/grid/">Bootstrap et ses 12 colonnes</a> se sont imposés dans le monde du design comme du développement depuis des années : il faut alors découper son site verticalement selon autant de colonne voulue.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Etape 1.bis : Trouver l'inspiration</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Du coup sans trop d'idée, il vaut mieux aller voir ce qu'il se fait de mieux en terme de design et suivre les tendances de l'époque (tout en gardant ses propres goûts).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Voici quelques pistes pour celles et ceux qui en souhaiteraient (vous pouvez bien sûr proposer vos propres ressources en commentaire, j'affinerais la liste en conséquence) :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><a href="https://www.blogduwebdesign.com">https://www.blogduwebdesign.com</a></li><li><a href="https://dribbble.com/">https://dribbble.com/</a></li><li><a href="https://www.awwwards.com/">https://www.awwwards.com/</a></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>On remarques plusieurs tendances : l'"offset" des éléments et du contenu, des titres avec des fonts assez grosses, des typos serifs qui ne sont plus combiné avec du sans-sérif et des bloc background qui se réalignent avec le contenu au fur et à mesure, ce qui contredit la tendance du premier point plus haut.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Etape 2 : Listing</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Pour commencer le sketching, il faut définir le contenu du site et ainsi les placer à la vue de l'utilisateur sans jamais les perdre. C'est tout l'objectif du design :&nbsp; le visuel au service du contenu.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Je commence ainsi un petit travail de listing :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Page d'accueil :&nbsp;<ul><li>Articles</li><li>Menu avec liens importants (accueil, catégories, cv, contact, réseaux)</li></ul></li><li>Catégories</li><li>Articles (complets et liens "en passant")</li><li>// Sidebar (déjà présente)</li><li>Contact</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Le nombre d'article est limité à 10 pour ne pas surcharger la page, puisque chaque article sera affiché en entier (jusqu'à une certaine longueur, mais en général, en entier).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Chaque article comporte : </p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Un titre</li><li>une image en avant</li><li>une date de publication et de modification</li><li>le contenu</li><li>les sources</li><li>partage réseaux</li><li>commentaires</li><li>tags</li><li>catégorie</li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Etape 3 - Sketching</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Pour entamer un sketching, sachant que ce n'est sans doute pas mon point fort, je ne peux que vous conseiller de vous renseigner mais de mon expérience personnelle :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>soit vous commencez à sketcher sur papier</li><li>soit directement en qualité basse sur un logiciel dédié</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Puisque je ne sais pas du tout dessiner, encore moins sketcher sur papier, je part sur la deuxième option avec Adobe XD (Sketch étant réservé à iOS).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Pour faire mon choix de couleur rapide, j'utilise <a href="https://coolors.co/ff7254-ffba49-20a39e-23001e-a4a9ad">Coolors </a>qui me génère une palette restreinte de couleur (j'incorpore celle de mon logo en premier puis génère le tout) et obtiens ceci au bout de plusieurs essai :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":53} -->
<figure class="wp-block-image"><img src="https://epistol.fr/wp-content/uploads/2018/11/ff7254-ffba49-20a39e-23001e-a4a9ad.png" alt="" class="wp-image-53"/><figcaption><br><em>(Et une palette scss pour plus tard dans notre thème Wordpress.)</em></figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Dans Adobe XD, chargeons la librairie <a href="https://www.adobe.com/fr/products/xd/resources.html#panel-3">"Kit de prototypage"</a>&nbsp;pour se donner des éléments de base pour faire notre low-res prototype, que je vous propose de retrouver dans le prochain article et ainsi réaliser la version "high-resolution" dans la foulée.</p>
<!-- /wp:paragraph -->