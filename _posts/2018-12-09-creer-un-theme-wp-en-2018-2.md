---
ID: 57
post_title: 'Créer un thème (WP) en 2018 &#8211;  2/3'
author: lm437747
post_excerpt: ""
layout: post
permalink: >
  https://epistol.fr/article/creer-un-theme-wp-en-2018-2/
published: true
post_date: 2018-12-09 14:20:55
---
<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>Cet article est la <a href="https://epistol.fr/article/47-creer-un-theme-wp-en-2018-1/">suite de l'épisode 1</a>, qui s'axe sur la recherche d'inspiration et de définition des objectifs.</p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>Après quelques heures de dessin et d'essais, voici mon résultat, à mi chemin entre low-res et high-res :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:gallery {"ids":[61,62]} -->
<ul class="wp-block-gallery columns-2 is-cropped"><li class="blocks-gallery-item"><figure><img src="https://i2.wp.com/blog.epistol.fr/wp-content/uploads/2018/11/Web-1920-–-1-1.png?fit=590%2C1024&amp;ssl=1" alt="" data-id="61" data-link="https://epistol.fr/?attachment_id=61" class="wp-image-61"/></figure></li><li class="blocks-gallery-item"><figure><img src="https://i2.wp.com/blog.epistol.fr/wp-content/uploads/2018/11/Web-1920-–-2.png?fit=590%2C1024&amp;ssl=1" alt="" data-id="62" data-link="https://epistol.fr/?attachment_id=62" class="wp-image-62"/></figure></li></ul>
<!-- /wp:gallery -->

<!-- wp:paragraph -->
<p>En termes de couleurs, on s'en tiens à 3 pour ne pas perdre les utilisateurs, on essaye de rester dans la tendance avec du offset avec "l'oeuf" sur le #Recap, et le background un peu excentré sur le titre de l'article, sans oublié l'effet vague sur le pied de page.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Etape 4 : Le développement</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Alors, et maintenant ? Il faut avoir son Wordpress installé en local, je vais pas vous faire un tuto ici,&nbsp; il en existe des <a href="https://www.themeum.com/install-wordpress-localhost/"><strong>TAS</strong></a> !</p>
<!-- /wp:paragraph -->

<!-- wp:more {"customText":"SUITE DE l'ARtICLE"} -->
<!--more SUITE DE l'ARtICLE-->
<!-- /wp:more -->

<!-- wp:paragraph -->
<p>Une fois tout ça installé, il nous faut récupérer un thème "blank" ou "à nu" si vous préférez. Pour cela :&nbsp;<a href="https://underscores.me/">https://underscores.me/ </a>, à télécharger (n'oubliez pas de valider l'option SCSS si possible) puis à installer sur votre WP.&nbsp; Et du coup, ça donne à peu près ça :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":65} -->
<figure class="wp-block-image"><img src="https://i0.wp.com/blog.epistol.fr/wp-content/uploads/2018/11/2018-11-18-23_47_47-Epistol-Blog-–-Un-site-utilisant-WordPress.png?fit=629%2C291&amp;ssl=1" alt="" class="wp-image-65"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Oui voilà, c'est pauvre, c'est le but ! Maintenant, ouvrez votre plus bel éditeur PHP / SCSS, comme PHPStorm :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":66} -->
<figure class="wp-block-image"><img src="https://i2.wp.com/blog.epistol.fr/wp-content/uploads/2018/11/2018-11-19-00_23_59-epiblog-C__xampp_htdocs_epiblog-..._wp-content_themes_epiblog_sass_style.scs_.png?fit=629%2C338&amp;ssl=1" alt="" class="wp-image-66"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Notre thème est bien installé, nous avons nos éléments bien séparé (voir <a href="https://medium.com/@audreyhacq/l-atomic-design-une-m%C3%A9thode-de-co-creation-prometteuse-bd9d5fc2b2ad">Atomic Design</a> ) et pour générer nos éléments, configurez votre Phpstorm via ce tuto : <a href="https://www.jetbrains.com/help/phpstorm/transpiling-sass-less-and-scss-to-css.html">lien</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"php"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="php" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">function get_stylesheet_uri() {
	$stylesheet_dir_uri = get_stylesheet_directory_uri();
	$stylesheet_uri = $stylesheet_dir_uri . '/sass/style.css';</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p><strong>Petite étape subsidiaire : </strong>je rajoute la librairie <a href="https://bulma.io">Bulma</a>&nbsp;pour ne pas avoir à réinventer la roue et aussi parce que c'est une très bonne librairie CSS.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Je l'utilise ainsi afin de redonner la structure prévue dans le sketch design :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>CREATION DU MENU</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Afin de faire coller le menu à ma bibliothèque CSS, j'ai du créer un Walker Personnalisé pour dire à Wordpress de ne pas générer de liste &lt;ul&gt;&lt;li&gt; mais bien de se conformer à la disposition comme suit :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"php"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="php" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">class Nav_Footer_Walker extends Walker_Nav_Menu
{
	function start_lvl(&amp;$output, $depth = 0, $args = array())
	{
		$indent = str_repeat("\t", $depth);
		$output .= "\n$indent\n";
	}

	function end_lvl(&amp;$output, $depth = 0, $args = array())
	{
		$indent = str_repeat("\t", $depth);
		$output .= "$indent\n";
	}

	function start_el(&amp;$output, $item, $depth = 0, $args = array(), $id = 0)
	{
		$indent = ($depth) ? str_repeat("\t", $depth) : '';
		$class_names = $value = '';
		$classes = empty($item->classes) ? array() : (array)$item->classes;
		$classes[] = 'menu-item-' . $item->ID;
		$class_names = join(' ', apply_filters('nav_menu_css_class', array_filter($classes), $item, $args));
		$class_names = $class_names ? ' class="' . esc_attr($class_names) . '"' : '';
		$id = apply_filters('nav_menu_item_id', 'menu-item-' . $item->ID, $item, $args);
		$id = $id ? ' id="' . esc_attr($id) . '"' : '';

		$is_current_item = array_search('current-menu-item', $item->classes) != 0 ? ' active' : '';


		$output .= $indent . '';
		$attributes = !empty($item->attr_title) ? ' title="' . esc_attr($item->attr_title) . '"' : '';
		$attributes .= !empty($item->target) ? ' target="' . esc_attr($item->target) . '"' : '';
		$attributes .= !empty($item->xfn) ? ' rel="' . esc_attr($item->xfn) . '"' : '';
		$attributes .= !empty($item->url) ? ' href="' . esc_attr($item->url) . '"' : '';

		$description = (!empty ($item->description) and 0 == $depth)
			? '&lt;small class="nav_desc">' . esc_attr($item->description) . '&lt;/small>' : '';

		$title = apply_filters('the_title', $item->title, $item->ID);
		if($args->walker->has_children) {
			$count = 1;
			$count++;
			$menu = $args->theme_location; // Getting the menu calling the walker from the array.
			$menu_items = wp_get_nav_menu_items($menu); // Getting the menu item objects array from the menu.
			$menu_item_parents = array_map(function($o) { return $o->menu_item_parent; }, $menu_items); // Getting the parent ids by looping through the menu item objects array. This will give an array of parent ids and the number of their children.
			$children_count = array_count_values($menu_item_parents)[$item->ID]; // Get number of children menu item has.

			/*if($children_count == $count) {
				var_dump("Je suis le dernier ! " . $count);
			}*/
			$item_output = $args->before;
				/*var_dump('&lt;pre>');
				var_dump($args);
				var_dump('&lt;/pre>');*/
			$item_output .= '&lt;div class="navbar-item has-dropdown is-hoverable">&lt;a' . $attributes . ' class="navbar-link '.$is_current_item.'">';
			$item_output .= $args->link_before . $title . $args->link_after;
			$item_output .= '&lt;/a>&lt;div class="navbar-dropdown is-boxed">';
			$item_output .= $args->after;
		} else {
			$item_output = $args->before;
			$item_output .= '&lt;a' . $attributes . ' class="navbar-item '.$is_current_item.'" >';
			$item_output .= $args->link_before . $title . $args->link_after;
			$item_output .= '&lt;/a>';
			$item_output .= $args->after;
		}

		$output .= apply_filters('walker_nav_menu_start_el', $item_output, $item, $depth, $args);
	}

	function end_el(&amp;$output, $item, $depth = 0, $args = array())
	{
		$output .= "\n";
	}
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Avec plusieurs arrangement CSS, l'ajout de mes fonts, voici le résultat pour le moment :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":100} -->
<figure class="wp-block-image"><img src="https://i0.wp.com/blog.epistol.fr/wp-content/uploads/2018/12/2018-12-07-22_45_59-Window.png?fit=629%2C281&amp;ssl=1" alt="" class="wp-image-100"/><figcaption>ça commence à ressembler à quelque chose ...</figcaption></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
<h3>LES ARTICLES</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Comme vous le voyez sur l'image précédente, j'ai appliqué un début de thème sur l'article, mais il manque le "colonnage" avec le menu latéral :&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":101} -->
<figure class="wp-block-image"><img src="https://epistol.fr/wp-content/uploads/2018/12/2018-12-07-22_51_01-Window.png" alt="" class="wp-image-101"/><figcaption>Suffit de passer son index.php avec des colonnes</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p><strong><em>Prochaines étapes : L'article "sticky" (récap) et le menu latéral !&nbsp;</em></strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Code source du thème :&nbsp;<a href="https://github.com/Epistol/EpiBlog-WP-Theme">https://github.com/Epistol/EpiBlog-WP-Theme</a></p>
<!-- /wp:paragraph -->