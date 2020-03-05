---
ID: 87
post_title: 'Passer un Objet dans un composant VueJS [TIPS]'
author: lm437747
post_excerpt: ""
layout: post
permalink: >
  https://epistol.fr/ressources/passer-un-objet-dans-un-composant-vuejs-tips/
published: true
post_date: 2018-12-06 10:26:50
---
<!-- wp:paragraph -->
<p>Bonsoir bonsoir, petite astuce pour ceux qui voudraient un jour passer un objet en tant qu'élément à afficher dans un composant VueJS (avec Laravel par exemple) :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Si votre Objet est un objet simple, vous devez le formaliser en json, comme ici avec un json_encode simple :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"php"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="php" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">     &lt;mini_recipe_list_element :recipe="{{json_encode($recette)}}">&lt;/mini_recipe_list_element>
</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Si jamais avec Laravel, votre Objet est issu d'une collection Eloquent, vous pouvez <a href="https://laravel.com/docs/5.7/eloquent-serialization#serializing-to-json">le sérialiser si ce n'est pas déjà fait :&nbsp;</a></p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"js"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="js" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">$user->toJson();</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Et ensuite dans votre composant VueJS, il faut lui dire qu'on attend un objet en tant que prop&nbsp; :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"js"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="js" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">props: {
			recipe: {
				type: Object,
				required: true
			}
		},</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Et voilà :)&nbsp;</p>
<!-- /wp:paragraph -->