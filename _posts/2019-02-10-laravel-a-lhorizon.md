---
ID: 145
post_title: 'Laravel à l&rsquo;Horizon'
author: Epistol
post_excerpt: ""
layout: post
permalink: >
  https://epistol.fr/ressources/laravel-a-lhorizon/
published: true
post_date: 2019-02-10 17:13:08
---
<!-- wp:paragraph -->
<p>Bonjour à tous et bienvenue dans ce tutoriel dédié à l'installation serveur et locale et l'utilisation d'Horizon pour Laravel.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Horizon est un tableau de bord pour gérer le système de file d'attente (<a href="https://laravel.com/docs/master/queues">queues</a>) de vos tâches (<a href="https://laravel.com/docs/master/queues#creating-jobs">jobs</a>) dans Laravel. </p>
<!-- /wp:paragraph -->

<!-- wp:more -->
<!--more-->
<!-- /wp:more -->

<!-- wp:paragraph -->
<p>Tout d'abord, Horizon repose sur le driver de queue Redis, qu'il faut donc installer : </p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"shell"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="shell" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">sudo apt-get install redis-server</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p><strong>Testez si celui-ci fonctionne et réagi : </strong></p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"shell"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="shell" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">redis-cli
ping //(retournera PONG)</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p><strong>Mettez à jour votre fichier .env : </strong></p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">QUEUE_CONNECTION=redis</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Pour un tutoriel plus poussé sur serveur, vous pouvez regarder <a href="https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-redis-on-ubuntu-18-04">ce tutoriel&nbsp;(pour&nbsp;Ubuntu&nbsp;16 et&nbsp;18)</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Il nous faut installer Supervisor pour que redis charge tout seul sur serveur : </strong></p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">sudo apt install supervisor
sudo service supervisor restart
sudo systemctl enable supervisord</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p><strong>Créer une configuration de Supervisor pour Horizon</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Superviseur conserve les fichiers individuels de ses programmes dans  </p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">/etc/supervisor/conf.d</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Il faut ainsi créer un fichier de config pour notre redis : </p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">sudo nano /etc/supervisor/conf.d/YOUR-APP-NAME-CHANGE-THIS.conf</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Et passer ce contenu : </p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">[program:laravel_horizon]
process_name=%(program_name)s_%(process_num)02d
command=php /home/ubuntu/YOUR-PROJECT-FOLDER-CHANGE-THIS/artisan horizon
autostart=true
autorestart=true
redirect_stderr=true
user=www-data
stdout_logfile=/home/ubuntu/YOUR-PROJECT-FOLDER-CHANGE-THIS/storage/horizon.log</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Plus qu'a redémarrer le superviseur : </p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">sudo supervisorctl reread
sudo supervisorctl update</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Et vérifier qu'il tourne : </p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">sudo supervisorctl</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Après chaque déploiement, il faut bien utiliser ces commandes (ou les intégrer dans votre pipeline de développement continu) : </p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">php artisan horizon:purge
php artisan horizon:terminate
php artisan horizon</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Et à partir de là, toutes vos tâches seront traitées par Horizon, sachez néanmoins que le dashboard disponible en local avec <code>/horizon</code> ne sera pas visible en <code>production</code> ! </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Sinon vous pouvez toujours utiliser <a href="https://www.cloudways.com/en/?id=375328">Cloudways</a> pour gérer vos déploiements automatiquement, leurs outils sont assez top.</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<a href="https://www.cloudways.com/en/laravel-hosting.php?id=375328&amp;a_bid=f2023ff7"><img src="https://epistol.fr/wp-content/uploads/2019/02/f2023ff7.jpg" alt="" class="wp-image-244"></a>
<!-- /wp:html -->

<!-- wp:html -->
<!-- Go to www.addthis.com/dashboard to customize your tools --> <div class="addthis_relatedposts_inline"></div>
<!-- /wp:html -->

<!-- wp:separator -->
<hr class="wp-block-separator"/>
<!-- /wp:separator -->

<!-- wp:html -->
<!-- Go to www.addthis.com/dashboard to customize your tools --> <div class="addthis_relatedposts_inline"></div>
<!-- /wp:html -->