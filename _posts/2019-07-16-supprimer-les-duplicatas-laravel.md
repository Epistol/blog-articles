---
ID: 400
post_title: Supprimer les duplicatas Laravel
author: Epistol
post_excerpt: ""
layout: post
permalink: >
  https://epistol.fr/ressources/supprimer-les-duplicatas-laravel/
published: true
post_date: 2019-07-16 18:08:48
---
<!-- wp:paragraph -->
<p>Petit snippet pour ceux qui se retrouve avec du bout de code qui n'a pas pris en compte le FirstOrCreate et une DB cracra avec des champs avec le même nom : </p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"php"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="php" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">$ingredients = DB::table('yourtable')->groupBy('name')
->pluck('id')->toArray();
$duplicated = DB::table('yourtable')->whereNotIn('id', $ingredients)->delete();</pre>
<!-- /wp:enlighter/codeblock -->