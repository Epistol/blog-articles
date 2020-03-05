---
ID: 370
post_title: Droits du dossier storage sur Fedora
author: Epistol
post_excerpt: ""
layout: post
permalink: >
  https://epistol.fr/ressources/droits-du-dossier-storage-sur-fedora/
published: true
post_date: 2019-06-18 18:36:34
---
<!-- wp:paragraph -->
<p>Quickie : si pour une raison ou une autre vous faites une nouvelle install Laravel et que vous avez besoin d'utiliser le folder session, sur fedora (linux), la bonne commande pour laisser Laravel faire son travail sera : </p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"shell"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="shell" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">sudo chmod -R guo+w storage</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Ce qui débloque les droit de lecture et écriture sur le dossier.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Bon dev à tous.</p>
<!-- /wp:paragraph -->