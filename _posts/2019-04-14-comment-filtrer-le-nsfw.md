---
ID: 339
post_title: Comment filtrer le NSFW ?
author: Epistol
post_excerpt: ""
layout: post
permalink: >
  https://epistol.fr/article/comment-filtrer-le-nsfw/
published: true
post_date: 2019-04-14 10:58:58
---
<!-- wp:paragraph -->
<p>Dans un soucis de rester en règles avec toutes celles qui déboulent sur internet depuis quelques temps mais aussi de se protéger soit-même quand on opère un site avec du contenu utilisateur, il est important d'appliquer des filtres NSFW. Mais comment, et à quel prix, on va tenter d'y voir un peu plus clair.</p>
<!-- /wp:paragraph -->

<!-- wp:more -->
<!--more-->
<!-- /wp:more -->

<!-- wp:paragraph -->
<p>En l'état, aujourd'hui, quand on veut développer un site et avec assez peu de moyens, il faut trouver des solutions pas trop chère ni difficile à intégrer tout en étant à jour, et c'est assez complexe de rassembler toutes ces qualités, mais avec la démocratisation de l'IA, c'est de plus en plus accessible, en tant qu'IA 'as-a-service' (ou AIAAS) !</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Dans notre shortlist (à date de publication) : </strong></p>
<!-- /wp:paragraph -->

<!-- wp:table {"hasFixedLayout":true,"className":"is-style-regular"} -->
<table class="wp-block-table has-fixed-layout is-style-regular"><tbody><tr><td></td><td><strong>SightEngine</strong></td><td><strong>Google Vision</strong></td><td><strong>Amazon <br>Rekognition</strong></td></tr><tr><td><em>Nombre <br>opérations <br>gratuits</em></td><td>2000 / mois (500/jr)</td><td>1000/mois</td><td>5000/mois</td></tr><tr><td><em>Tarifs au dela</em></td><td>30$/mois (max 10k opérations)</td><td>$1.50 / opérations (max 5 millions)</td><td>1$ par tranche de 1000 images</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:paragraph -->
<p>L'un des grands gagnants qui ressort de cette petite analyse reste Amazon, suivi par SightEngine avec une offre claire, et Google Vision qui possède l'un des plus efficace moteur de détections, mais reste horriblement cher dès que nous dépassons les 1000 opérations mensuelles.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Utilisation de l'IA</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Pour notre exemple, nous utiliseront SightEngine et le framework Laravel (ça faisait longtemps) : </p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"php"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="php" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">$sightEngine = new SightengineClient(env('SIGHTENGINEUSER'), env('SIGHTENGINEKEY'));
$imageCheck = $sightEngine->check(['nudity', 'wad', 'offensive', 'face-attributes', 'text'])->set_file($picture);</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Ce qui nous renverra un JSON avec l'analyse de SightEngine, libre à vous d'en faire ce que vous voulez, moi je met les images à la poubelle quand le taux de chaque filtre est supérieur à 0,85, juste histoire de pas avoir à modérer trop de contenu, et les quelques faux positifs seront peu nombreux.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Have fun avec tout les outils et tout ce que vous pouvez coder avec ça donc, n'oubliez surtout pas les formulaires de réclamation en cas de faux-positif pour les utilisateurs. Pas comme Youtube quoi.</p>
<!-- /wp:paragraph -->