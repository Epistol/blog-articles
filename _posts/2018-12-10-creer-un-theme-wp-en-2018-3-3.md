---
ID: 105
post_title: Créer un thème (WP) en 2018 – 3/3
author: lm437747
post_excerpt: ""
layout: post
permalink: >
  https://epistol.fr/article/creer-un-theme-wp-en-2018-3-3/
published: true
post_date: 2018-12-10 18:12:13
---
<!-- wp:quote -->
<blockquote class="wp-block-quote"><p><em>Cet article est la&nbsp;</em><a href="https://epistol.fr/article/57-creer-un-theme-wp-en-2018-2/">suite de l'épisode 2</a><em>, qui s'axait sur la mise en page du thème et l'installation du design.</em></p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>Suite et grosse fin de notre série sur le développement d'un thème simple pour Wordpress :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Notre thème majoritaire est conçu, on va s'attaquer à l'article "Sticky", celui qui reste en haut de la page sur une période définie, et qui sera pour moi un petit article dans la veine de Korben pour faire une mini news récapitulative de la semaine et d'autres trucs.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>STICKY ARTICLE</h2>
<!-- /wp:heading -->

<!-- wp:more -->
<!--more-->
<!-- /wp:more -->

<!-- wp:paragraph -->
<p>Dans mon dossier Template Parts, je créé un nouveau template "sticky" pour pouvoir le charger différement de content.php dans notre index.php :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"php"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="php" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">&lt;?php
/**
 * The main template file
 *
 * This is the most generic template file in a WordPress theme
 * and one of the two required files for a theme (the other being style.css).
 * It is used to display a page when nothing more specific matches a query.
 * E.g., it puts together the home page when no home.php file exists.
 *
 * @link https://developer.wordpress.org/themes/basics/template-hierarchy/
 *
 * @package Epistol_Blog
 */

get_header();
?>

&lt;?php
if(have_posts()) :
	if(is_home() &amp;&amp; !is_front_page()) :
		?>
        &lt;header>
            &lt;h1 class="page-title screen-reader-text">&lt;?php single_post_title(); ?>&lt;/h1>
        &lt;/header>
	&lt;?php
	endif;

	/* Start the Loop */
	while(have_posts()) :
		the_post();
		if(is_sticky()) {
			// On charge notre nouveau template sticky
			get_template_part('template-parts/sticky', get_post_type());
		}

	endwhile;
	the_posts_navigation();
else :
	get_template_part('template-parts/content', 'none');
endif;
?>
    &lt;div class="columns">
        &lt;div class="column is-8 ">
            &lt;div id="primary" class="content-area">
                &lt;main id="main" class="site-main">

					&lt;?php
					if(have_posts()) :
						if(is_home() &amp;&amp; !is_front_page()) :
							?>
                            &lt;header>
                                &lt;h1 class="page-title screen-reader-text">&lt;?php single_post_title(); ?>&lt;/h1>
                            &lt;/header>
						&lt;?php
						endif;

						/* Start the Loop */
						while(have_posts()) :
							the_post();

							if(!is_sticky()) {
// si l'article n'est pas sticky : 
								get_template_part('template-parts/content', get_post_type());

							}
						endwhile;
						the_posts_navigation();
					else :
						get_template_part('template-parts/content', 'none');
					endif;
					?>

                &lt;/main>&lt;!-- #main -->
            &lt;/div>&lt;!-- #primary -->
        &lt;/div>
        &lt;div class="column">
			&lt;?php get_sidebar();
			?>
        &lt;/div>
    &lt;/div>


&lt;?php
get_footer();
</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Afin de faire correspondre l'image mis en avant avec le design créé dans Adobe XD, on va utiliser le mask-clip css sur notre image :</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"css"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="css" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">.mask {
	-webkit-mask-image: url(../img/mask.svg);
	mask-image: url(../img/mask.svg);
	mask-repeat: no-repeat;
	-webkit-mask-repeat: no-repeat;
}
</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Bon, éventuellement j'aimerais bien l'animer un peu mais on verra plus tard, pour l'instant on à ça :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":106} -->
<figure class="wp-block-image"><img src="https://i2.wp.com/blog.epistol.fr/wp-content/uploads/2018/12/2018-12-09-15_03_20-Epistol-Blog-Un-site-utilisant-WordPress.png?fit=629%2C263&amp;ssl=1" alt="" class="wp-image-106"/><figcaption>Pas très organisé encore</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>On rajoute "sticky" en tant que class css à tout les élements voulu et l'image en position absolute, et voilà :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":107} -->
<figure class="wp-block-image"><img src="https://i0.wp.com/blog.epistol.fr/wp-content/uploads/2018/12/2018-12-09-15_23_02-Epistol-Blog-Un-site-utilisant-WordPress.png?fit=629%2C311&amp;ssl=1" alt="" class="wp-image-107"/><figcaption>Nice</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Tout n'est pas encore parfait, mais c'est des finitions qui viendront plus tard, on va d'abord s'attaquer au menu latéral pour finir par le footer.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Menu latéral : peu de chose à changer, des couleurs et du padding.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>FOOTER</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Au début, je voulais tenter un svg mask mais pour préserver la compatilibité de tout les navigateurs, on va juste faire un svg en tant qu'image chargée juste avant le footer et remonter le footer avec un margin négatif : </p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"php"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="php" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">
&lt;/div>&lt;!-- #page -->
&lt;img src="&lt;?= get_template_directory_uri()?>/img/footer-01.svg" />

&lt;footer id="colophon" class="site-footer"></pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:enlighter/codeblock {"language":"css"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="css" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">footer#colophon {
  background: #FF7254;
  position: absolute;
  margin-top: -1rem;
  color: white;
  padding: 1rem;
  z-index: 0;
  min-height: 20vh;
  width: 100%;
 
}

</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Et voilà, la majorité du thème est réalisé, petite finitions à droite  à gauche, et calquer le thème index sur les autres templates mais enfin en gros, tout est réalisé. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Merci d'avoir suivi ce tuto, n'hésitez pas à commenter et partager cet article !</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><em>NB : Thème disponible sur </em><a href="https://github.com/Epistol/EpiBlog-WP-Theme"><em>Github</em></a></p>
<!-- /wp:paragraph -->