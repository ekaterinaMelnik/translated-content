---
title: Gérer les problèmes courants d'accessibilité
slug: Learn/Tools_and_testing/Cross_browser_testing/Accessibility
tags:
  - Accessibilité
  - Apprentissage
  - Article
  - CSS
  - Clavier
  - Débutant
  - HTML
  - JavaScript
  - Outils
  - navigateur croisé
  - test
translation_of: Learn/Tools_and_testing/Cross_browser_testing/Accessibility
original_slug: Learn/Tools_and_testing/Cross_browser_testing/Accessibilité
---
<div>{{LearnSidebar}}</div>

<div>{{PreviousMenuNext("Learn/Tools_and_testing/Cross_browser_testing/JavaScript","Learn/Tools_and_testing/Cross_browser_testing/Feature_detection", "Learn/Tools_and_testing/Cross_browser_testing")}}</div>

<p>Tournons maintenant notre attention vers l'accessibilité, les informations sur les problèmes communs, comment faire des tests simples, et comment faire pour utiliser les outils d'audit/automatisation pour trouver les problèmes d'accessibilités.</p>

<table class="standard-table">
 <tbody>
  <tr>
   <th scope="row">Prérequis :</th>
   <td>
    <p>Connaissances avec le noyau des langages <a href="/fr/Apprendre/HTML">HTML</a>, <a href="/fr/Apprendre/CSS">CSS</a> et <a href="/fr/Apprendre/JavaScript">JavaScript</a> ; une idée du haut niveau des principes du <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Introduction">test en navigateur croisé</a>.</p>
   </td>
  </tr>
  <tr>
   <th scope="row">Objectif :</th>
   <td>
    <p>Être capable de diagnostiquer les problèmes courants d'Accessibilité, et utiliser les outils et techniques appropriés pour les résoudre.</p>
   </td>
  </tr>
 </tbody>
</table>

<h2 id="Qu'est-ce_que_l'accessibilité">Qu'est-ce que l'accessibilité ?</h2>

<p>Quand on parle d'accessibilité dans le contexte de la technologie web, la plupart des gens pense directement au fait de s'assurer que les sites web/apps sont utilisables par les personnes avec des handicap, par exemple :</p>

<ul>
 <li>Les personnes malvoyantes utilisant des lecteurs d'écran ou l'élargissement/zoom pour accéder au texte.</li>
 <li>Les personnes avec des troubles fonctionnels moteurs utilisant le clavier (ou d'autres fonctions sans souris) pour activer des fonctionnalités de site web.</li>
 <li>Les personnes avec des troubles auditifs dépendant des légendes/sous-titres ou d'autres textes alternatifs pour du contenu audio/vidéo.</li>
</ul>

<p>Toutefois, ce serait faux de réduire l'accessibilité uniquement aux handicaps. Le vrai but de l'accessibilité est de faire en sorte que vos sites web/applis soient utilisables par le plus grand nombre de personnes dans le plus grand nombre de contextes possibles, pas uniquement ces utilisateurs qui utilisant des ordinateurs de bureau puissants. Les exemples extrêmes pourraient inclure :</p>

<ul>
 <li>Les utilisateurs sur des appareils mobiles.</li>
 <li>Les utilisateurs sur des appareils de navigation alternatifs comme les TVs, les montres, etc.</li>
 <li>Les utilisateurs de vieux appareils qui n'ont pas les derniers navigateurs.</li>
 <li>Les utilisateurs avec des appareils aux caractéristiques basses qui peuvent avoir des processeurs lents.</li>
</ul>

<p>D'une certaine manière, la totalité de ce module concerne l'accessibilité — le test en navigateur croisé assure que vos sites peuvent être utilisé par le plus de personne possible. <a href="/fr/Apprendre/a11y/What_is_accessibility">Qu'est-ce que l'accessibilité ?</a> décrit plus largement et précisément l'accessibilité que cet article ne le fait.</p>

<p>Cela dit, cet article couvrira les problèmes en navigateur croisé et de test entourant les personnes avec des handicaps, et comment ils utilisent le Web. Nous avons déjà parlé des autres domaines comme le <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/HTML_et_CSS#Les_probl%C3%A8mes_de_responsive_design">responsive design</a> et la <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/JavaScript#Les_probl%C3%A8mes_de_performance">performance</a> à d'autres endroits dans ce module.</p>

<div class="note">
<p><strong>Note :</strong> Comme beaucoup de choses dans le développement web, l'accessibilité ne concerne pas la totale réussite ou échec ; l'accessibilité à 100% est quasiment impossible à atteindre pour tous les contenus, spécialement quand les sites deviennent plus complexes. Il s'agit plutôt de faire un effort pour rendre votre contenu accessible au plus grand nombre de personnes possible, avec du code de prévention, et se tenir aux meilleures pratiques.</p>
</div>

<h2 id="Problèmes_d'accessibilité_courants">Problèmes d'accessibilité courants</h2>

<p>Dans cette section nous détaillerons certains des problèmes principaux qui se manifestent autour de l'accessibilité, liée à des technologies spécifiques, avec les bonnes pratiques à adopter, et quelques tests rapides que vous pouvez faire pour voir si vos sites vont dans le bon sens.</p>

<div class="note">
<p><strong>Note :</strong> L'accessibilité est moralement la bonne chose à faire, est bonne pour les affaires (nombre élevé d'utilisateurs handicapés, utilisateurs sur des appareils mobiles, etc. représentent un segment du marché signifiant), mais c'est aussi illégal dans de nombreuses régions de la planète de ne pas rendre les propriétés du web accessibles aux personnes avec des handicaps. Pour plus d'informations, lisez <a href="/fr/docs/Learn/Accessibility/What_is_accessibility#Accessibility_guidelines_and_the_law">Accessibility guidlines and the law</a>.</p>
</div>

<h3 id="HTML">HTML</h3>

<p>La sémantique HTML (où les éléments sont utilisés à leur fin prévues) est accessible sans aucune modification — les contenus sont lisibles par les spectateurs voyants (à condition que vous n'ayez rien fait d'absurde comme rendre le texte bien trop petit ou ne l'ayez caché en utilisant du CSS), mais il sera aussi utilisable par des technologies d'assistance comme les lecteurs d'écran (applis qui lisent littéralement une page à leurs utilisateurs), et apporte également d'autres avantages.</p>

<h4 id="La_structure_sémantique">La structure sémantique</h4>

<p>Le quick win le plus important en sémantique HTML et d'utiliser une structure de rubriques et de paragraphes pour votre contenu ; parce que les utilisateurs de lecteurs d'écran ont tendance à utiliser les rubriques d'un document comme indications pour trouver le contenu qu'il recherche plus rapidement. Si votre contenu n'a pas de rubriques, tout ce qu'ils auraient c'est un énorme mur de texte sans aucune indication pour trouver quelque chose. Exemples de bon et de mauvais HTML :</p>

<pre class="brush: html example-bad">&lt;font size="7"&gt;My heading&lt;/font&gt;
&lt;br&gt;&lt;br&gt;
This is the first section of my document.
&lt;br&gt;&lt;br&gt;
I'll add another paragraph here too.
&lt;br&gt;&lt;br&gt;
&lt;font size="5"&gt;My subheading&lt;/font&gt;
&lt;br&gt;&lt;br&gt;
This is the first subsection of my document. I'd love people to be able to find this content!
&lt;br&gt;&lt;br&gt;
&lt;font size="5"&gt;My 2nd subheading&lt;/font&gt;
&lt;br&gt;&lt;br&gt;
This is the second subsection of my content. I think is more interesting than the last one.</pre>

<pre class="brush: html example-good">&lt;h1&gt;My heading&lt;/h1&gt;

&lt;p&gt;This is the first section of my document.&lt;/p&gt;

&lt;p&gt;I'll add another paragraph here too.&lt;/p&gt;

&lt;h2&gt;My subheading&lt;/h2&gt;

&lt;p&gt;This is the first subsection of my document. I'd love people to be able to find this content!&lt;/p&gt;

&lt;h2&gt;My 2nd subheading&lt;/h2&gt;

&lt;p&gt;This is the second subsection of my content. I think is more interesting than the last one.&lt;/p&gt;</pre>

<p>De plus, votre contenu doit avoir un sens logique dans son code source — vous pourrez toujours le placer où vous voulez en utilisant du CSS plus tard, mais vous devez avoir un bon code source avec lequel commencer.</p>

<p>Comme test, vous pouvez désactiver le CSS d'un site et voir à quel point il est compréhensible sans ce dernier. Vous pouvez le faire manuellement juste en retirant le CSS de votre code, mais la façon la plus simple reste d'utiliser les fonctionnalités du navigateur, par exemple :</p>

<ul>
 <li>Firefox : Sélectionnez <em>Affichage &gt; Style de page &gt; Aucun style</em> depuis le menu principal.</li>
 <li>Safari : Sélectionnez <em>Développement &gt; Désactiver les styles</em> depuis le menu principale (pour activer le menu <em>Développement</em>, choisissez <em>Safari </em>&gt; <em>Préférences </em>&gt; <em>Avancés </em>&gt; <em>Montrer le menu développement dans la barre de menu</em>).</li>
 <li>Chrome : Installez l'extension Web Developer Toolbar, puis redémarrer le navigateur. Cliquez sur l'icône engrenage qui apparaîtra, puis sélectionnez <em>CSS</em> &gt; <em>Désactiver tous les styles.</em></li>
 <li>Edge : Sélectionnez <em>Vue </em>&gt; <em>Style</em> &gt; <em>Aucun style</em> depuis le menu principal.</li>
</ul>

<h4 id="Utiliser_l'accessibilité_native_du_clavier">Utiliser l'accessibilité native du clavier</h4>

<p>Certaines fonctionnalités HTML peuvent être sélectionnées en utilisant uniquement le clavier — c'est le comportement par défaut, disponible depuis les prémices du web. Les éléments qui ont cette capacité sont les plus communs qui permettent à l'utilisateur d'interagir avec les pages web, à savoir les liens, {{htmlelement("button")}}s, et les éléments des formulaire comme {{htmlelement("input")}}.</p>

<p>Vous pouvez essayer ceci en utilisant notre exemple <a href="http://mdn.github.io/learning-area/tools-testing/cross-browser-testing/accessibility/native-keyboard-accessibility.html">native-keyboard-accessibility.html</a> (voir le <a href="https://github.com/mdn/learning-area/blob/master/tools-testing/cross-browser-testing/accessibility/native-keyboard-accessibility.html">code source</a>) — ouvrez le dans un nouvel onglet, et essayez de presser la touche tab ; après quelques pressions, vous devriez voir la focalisation du tab commencer à se déplacer entre les différents éléments focalisables ; les éléments focalisés ont un style de mise en avant par défaut dans tous les navigateurs (cela diffère peu entre les différents navigateurs) donc vous pouvez dire quel éléments est focalisé.</p>

<p><img alt="" src="button-focused-unfocused.png"></p>

<p>Vous pouvez ensuite presser Entrée/Retour pour accéder à un lien focalisé ou presser un bouton (nous avons inclus un peu de JavaScript pour que les boutons renvoies un message d'alerte), ou commencer à taper pour entrer du texte dans un des input texte (d'autres éléments de formulaire ont différents contrôles, par exemple l'élément {{htmlelement("select")}} peut avoir ses options affichées et navigable en utilisant les touches haut et bas).</p>

<p>Notez que différents navigateurs peuvent avoir différentes options de contrôle par clavier disponibles. La plupart des navigateurs modernes respectent le modèle de tab écrit plus haut (vous pouvez aussi faire une Shift + Tab pour reculer entre les éléments focalisables), mais certains navigateurs ont leurs propres particularités :</p>

<ul>
 <li>Firefox pour Max ne tabule pas par défaut. Pour l'activer, vous devez aller dans <em>Préférences</em> &gt; <em>Avancées</em> &gt; <em>Général</em>, puis décochez "Toujours utiliser les curseurs pour naviguer dans une page". Ensuite, vous devez ouvrir les Préférences Système de votre Mac, puis sélectionnez le boutons radio <em>Tous les contrôles</em>.</li>
 <li>Safari ne vous permet pas de naviguer avec tab par défaut ; pour l'activer, vous devez ouvrir les <em>Préférences</em> de Safari, allez dans Avancées, et cochez la case à cocher <em>Presser tab pour mettre en avant chaque item sur une page web</em>.</li>
</ul>

<div class="warning">
<p><strong>Attention :</strong> Vous devez jouer ce genre de test sur toutes les pages que vous écrivez — assurez-vous que la fonctionnalité peut être accessible par le clavier.</p>
</div>

<p>Cet exemple souligne l'importance de l'utilisation de la sémantique correcte d'élément pour le travail correct. C'est possible de styler <em>n'importe quel</em> élément pour qu'il ressemble à un lien ou un bouton avec le CSS, et de le faire se comporter comme un lien ou un bouton avec JavaScript, mais ils ne seront toujours pas des liens ou des boutons, et vous perdrez beaucoup de l'accessibilité que ces éléments vous fournissent pour rien. Donc ne le faîte pas si vous pouvez l'éviter.</p>

<p>Un autre conseil — comme vu dans notre exemple, vous pouvez contrôler comment vos éléments focalisables paraissent quand ils sont focalisés, en utilisant la pseudo-class <a href="/fr/docs/Web/CSS/:focus">:focus</a>. C'est une bonne idée de doubler les styles focus et hover, comme ça vos utilisateurs auront un indice visuel qu'un contrôle fera quelque chose lorsqu'il sera activé, qu'ils utilisent la souris ou le clavier :</p>

<pre class="brush: css">a:hover, input:hover, button:hover, select:hover,
a:focus, input:focus, button:focus, select:focus {
  font-weight: bold;
}</pre>

<div class="note">
<p><strong>Note :</strong> Si vous décidez de retirer le style focus par défaut en utilisant du CSS, assurez-vous de le remplacer par autre chose qui s'accorde au mieux avec votre design — c'est un outil d'accessibilité de grande valeur, qui ne doit pas être supprimé.</p>
</div>

<h4 id="Intégrer_l'accessibilité_clavier">Intégrer l'accessibilité clavier</h4>

<p>Parfois ça n'est pas possible d'éviter la perte de l'accessibilité clavier. Vous pouvez avoir hérité d'un site où la sémantique n'est pas parfaite (peut-être que vous vous êtes retrouvé avec un CMS horrible qui génère des boutons créés avec des <code>&lt;div&gt;</code>s), ou que vous utilisez un contrôle complexe qui n'a pas d'accessibilité clavier intégré, comme l'élément {{htmlelement("video")}} (étonnamment, Opera est le seul navigateur qui vous permet de tabuler dans l'élément <code>&lt;video&gt;</code> avec les contrôles par défaut du navigateur). Vous avez quelques options ici :</p>

<ol>
 <li>Créer des contrôles personnalisés en utilisant les éléments <code>&lt;button&gt;</code> (sur lequel nous pouvons tabuler par défaut !) et JavaScript pour les relier à leur fonction. Pour des bons exemples voir <a href="/fr/docs/Web/Apps/Fundamentals/Audio_and_video_delivery/cross_browser_video_player">Creating a cross-browser video player</a>.</li>
 <li>Créer des raccourcis clavier en utilisant JavaScript, les fonctions sont activés quand vous appuyez sur une certaine touche du clavier. Voir <a href="/fr/docs/Games/Techniques/Control_mechanisms/Desktop_with_mouse_and_keyboard">Desktop mouse and keyboard controls</a> pour des exemples en rapport avec le jeu qui peuvent être adaptés à d'autres fins.</li>
 <li>Utilisez des approches intéressantes pour simuler le comportement d'un bouton. Prenez par exemple notre exemple <a href="http://mdn.github.io/learning-area/tools-testing/cross-browser-testing/accessibility/fake-div-buttons.html">fake-div-buttons.html</a> (voir le <a href="https://github.com/mdn/learning-area/blob/master/tools-testing/cross-browser-testing/accessibility/fake-div-buttons.html">code source</a>). Nous donnons à nos faux boutons <code>&lt;div&gt;</code> la capacité d'être focalisé (y compris avec la tabulation) en donnant à chacun d'entre eux l'attribut <code>tabindex="0"</code> (voir l'<a href="https://webaim.org/techniques/keyboard/tabindex">article tabindex</a> de WebAIM pour plus de détails utiles). Cela nous permet de tabuler sur les boutons, mais pas de les activer avec la toucher Entrée/Retour. Pour faire cela, nous devons ajouter ce petit bout de tromperie en JavaScript :</li>
 <li>
  <pre class="brush: js">document.onkeydown = function(e) {
  if(e.keyCode === 13) { // The Enter/Return key
    document.activeElement.onclick(e);
  }
};</pre>
  Ici nous ajoutons un listener à l'objet <code>document</code> pour détecter quand une touche a été appuyée sur le clavier. Nous vérifions quelle touche a été pressée avec la propriété d'évènement d'objet <a href="/fr/docs/Web/API/KeyboardEvent/keyCode">keyCode</a> ; si c'est le code de la touche qui retourne Entrée/Retour, on exécute la fonction stockée dans le <code>onclick</code> du bouton en utilisant <code>document.activeElement.onclick()</code>. <code><a href="/fr/docs/Web/API/Document/activeElement">activeElement</a></code> nous donne l'élément courant qui est focalisé sur la page.</li>
</ol>

<div class="note">
<p><strong>Note :</strong> Cette technique ne fonctionnera que si vous configurer vos propres gestionnaires d'évènement avec les propriétés de gestion d'évènement (par ex. <code>onclick</code>). <code>addEventListener</code> ne fonctionnera pas. C'est beaucoup de prises de tête pour construire la fonctionnalité de retour. Et il y a d'autres problèmes rattachés avec. Vaut mieux commencer par utiliser les bons éléments pour leurs buts initiaux.</p>
</div>

<h4 id="Les_textes_alternatifs">Les textes alternatifs</h4>

<p>Les textes alternatifs sont très importants pour l'accessibilité — si une personne a un trouble visuel ou auditif qui l'empêche de voir ou d'entendre un contenu, alors c'est un problème. Le texte alternatif le plus simple disponible est le modeste attribut <code>alt</code>, que nous devrions inclure dans toutes les images qui contiennent un contenu pertinent. Il peut contenir une description de l'image qui transmet clairement son sens et son contenu sur la page, pour être récupéré par un lecteur d'écran et lu à l'utilisateur.</p>

<div class="note">
<p><strong>Note :</strong> Pour plus d'informations, lisez <a href="/fr/docs/Learn/Accessibility/HTML#Text_alternatives">Text alternatives</a>.</p>
</div>

<p>L'oubli de texte alt peut être testé de bien des façons, par exemple en utilisant le {{anch("Auditing tools")}} d'accessibilité.</p>

<p>Le texte alt est légèrement plus complexe pour du contenu vidéo ou audio. Il y a une manière de gérer l'affichage du texte (par ex. les sous-titres) et de les afficher quand la vidéo est jouée, sous le forme de l'élément {{htmlelement("track")}}, et du format <a href="/fr/docs/Web/API/Web_Video_Text_Tracks_Format">WebVTT</a> (voir <a href="/fr/Apps/Build/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video">Ajouter des légendes et des sous-titres à des vidéos HTML5</a> pour un tutoriel détaillé). <a href="/fr/Apps/Build/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video#Compatibilit%C3%A9_entre_navigateurs">La compatibilité entre navigateur</a> pour cette fonction est assez bonne, mais si vous voulez fournir des textes alternatifs pour de l'audio ou supporter les vieux navigateurs, une simple transcription du texte présenté quelque part sur la page ou sur une page séparée peut être une bonne idée.</p>

<h4 id="Relations_et_contexte_entre_élément">Relations et contexte entre élément</h4>

<p>Il y a certaines caractéristiques et pratiques optimales en HTML conçues pour apporter du contexte et des relations entre des éléments lorsqu'aucune n'aurait autrement existé. Les trois exemples les plus courants sont les liens, les libellés de formulaire et les tableau de données.</p>

<p>La solution pour les textes de type lien c'est que les personnes utilisant des lecteurs d'écran vont souvent utiliser une fonctionnalité commune avec laquelle ils vont récupérer une liste de tous les liens sur la page. Par exemple, une liste de lien libellés "cliquez ici", "cliquez ici", etc. est vraiment mauvaise pour l'accessibilité. Il est préférable pour les textes de type lien d'avoir du sens en contexte et hors contexte.</p>

<p>Le suivant sur notre liste, l'élément de formulaire {{htmlelement("label")}} est une des fonctionnalités centrales qui nous permet de rendre les formulaires accessibles. Le problème avec les formulaires c'est que vous avez besoin de libellés pour dire quelle donnée doit être entrée dans chaque champs du formulaire. Chaque libellé doit être inclus dans un {{htmlelement("label")}} pour le relier clairement à son champs partenaire (chaque valeur de l'attribut <code>for</code> de <code>&lt;label&gt;</code> doit aller avec la valeur de l'<code>id</code> de l'élément du formulaire), et cela aura du sens même si le code source n'est pas totalement logique (ce qui pour être tout à fait juste devrait être fait).</p>

<div class="note">
<p><strong>Note :</strong> Lisez <a href="/fr/docs/Learn/Accessibility/HTML#Meaningful_text_labels">Meaningful text labels</a>, pour plus d'information à propos des textes de type lien et les libellés des formulaires.</p>
</div>

<p>Pour terminer, un mot rapide sur les tableaux de données. Un tableau de données basique peut être écrit avec des indications très simples (voir <code>bad-table.html</code> <a href="http://mdn.github.io/learning-area/accessibility/html/bad-table.html">en direct</a>, et <a href="https://github.com/mdn/learning-area/blob/master/accessibility/html/bad-table.html">la source</a>), mais il y a des problèmes — il n'y a aucun moyen pour un utilisateur de lecteur d'écran d'associer des lignes ou des colonnes ensembles comme un groupe de données — pour faire cela vous devez connaître les lignes d'en-têtes, et si elles se dirigent en lignes, colonnes, etc. Cela ne peut être fait qu'en visuel pour un tel tableau.</p>

<p>Si vous regardez plutôt notre exemple <code>punk-band-complete.html</code> (<a href="https://mdn.github.io/learning-area/css/styling-boxes/styling-tables/punk-bands-complete.html">direct</a>, <a href="https://github.com/mdn/learning-area/blob/master/css/styling-boxes/styling-tables/punk-bands-complete.html">source</a>), vous pouvez voir plusieurs aides à l'accessibilité en place, comme les entêtes de tableau ({{htmlelement("th")}} et les attributs <code>scope</code>), l'élément {{htmlelement("caption")}}, etc.</p>

<div class="note">
<p><strong>Note :</strong> Lisez <a href="/fr/docs/Learn/Accessibility/HTML#Accessible_data_tables">Accessible data tables</a>, pour plus d'information à propos des tableaux accessibles.</p>
</div>

<h3 id="CSS">CSS</h3>

<p>Le CSS tend à fournir beaucoup moins de caractéristiques fondamentales d'accessibilité que le HTML, mais il peut aussi faire beaucoup de dommage à l'accessibilité s'il est mal utilisé. Nous avons déjà mentionné quelques conseils sur l'accessibilité incluant le CSS :</p>

<ul>
 <li>Utilisez les éléments sémantiques correctes pour définir différent contenu en HTML ; si vous voulez créer un effet visuel différent, utilisez le CSS — n'abusez pas d'un élément HTML pour obtenir l'aspect que vous désirez. Par exemple si vous voulez un texte plus gros, utilisez {{cssxref("font-size")}}, par un élément {{htmlelement("h1")}}.</li>
 <li>Assurez-vous que votre code source a du sens sans le CSS ; vous pouvez toujours utilisez le CSS pour styler autant que vous voudrez après.</li>
 <li>Vous devez vous assurez que les éléments interactifs comme les boutons et les liens ont des états focus/hover/active appropriés configuré, pour donner à l'utilisateur un indice visuel de leur fonction. Si vous supprimez les styles par défaut pour des raisons stylistiques, assurez-vous de mettre en place des styles de remplacement.</li>
</ul>

<p>Il y a quelques autres considérations que vous devriez prendre en compte.</p>

<h4 id="Couleur_et_contraste">Couleur et contraste</h4>

<p>Lorsque vous choisissez une palette de couleurs pour votre site web, vous devez vous assurer que la couleur du texte (au premier plan) contraste bien avec la couleur d'arrière-plan. Votre design peut avoir l'air cool, mais ce n'est pas bon si les personnes avec un handicap visuel comme le daltonisme ne peuvent pas lire votre contenu. Utilisez un outil comme le <a href="http://webaim.org/resources/contrastchecker/">Color Contrast Checker</a> de WebAIM si votre palette contraste suffisamment.</p>

<p>Une autre astuce est de ne pas compter sur une couleur seule pour les indications/informations, comme ça ne sera pas bon pour ceux qui ne peuvent pas voir la couleur. Plutôt que de marquer en rouge les champs requis d'un formulaire, par exemple, marquez-les avec un astérisque et en rouge.</p>

<div class="note">
<p><strong>Note :</strong> un contraste élevé permettra également à toute personnes utilisant un smartphone ou une tablette avec un écran brillant de mieux lire les pages dans un environnement lumineux, comme avec la lumière du soleil.</p>
</div>

<h4 id="Cacher_du_contenu">Cacher du contenu</h4>

<p>Il y a plusieurs cas où un design visuel requerra que tout le contenu ne soit pas montré d'un seul coup. Par exemple, dans notre <a href="http://mdn.github.io/learning-area/css/css-layout/practical-positioning-examples/info-box.html">Exemple de boîte d'info avec onglets</a> (voir le <a href="https://github.com/mdn/learning-area/blob/master/css/css-layout/practical-positioning-examples/info-box.html">code source</a>) nous avons trois panneau d'information, mais nous les <a href="/fr/docs/Learn/CSS/CSS_layout/Positioning">positionnons</a> les uns sur les autres et fournissons des onglets qui peuvent être cliqués pour montrer chacun d'entre eux (c'est aussi accessible au clavier — vous pouvez utiliser alternativement Tab et Entrée/Retour pour les sélectionner).</p>

<p><img alt="" src="tabbed-info-box.png"></p>

<p>Les utilisateurs de lecteur d'écran ne se soucient pas vraiment de cela — ils sont satisfaits tant que le contenu a du sens dans le code source, et qu'ils peuvent entièrement y accéder. Le positionnement absolute (comme utilisé dans cet exemple) est souvent vu comme l'un des meilleur mécanismes pour cacher du contenu pour des effets visuels, parce que ça n'empêche pas les lecteur d'écran d'y accéder.</p>

<p>D'un autre côté, vous ne devriez pas utiliser {{cssxref("visibility")}}<code>:hidden</code> ou {{cssxref("display")}}<code>:none</code>, parce qu'il cache le contenu aux lecteurs d'écran. A moins que, bien entendu, il y est une bonne raison qui justifie que ce contenu soit caché aux lecteurs d'écran.</p>

<div class="note">
<p><strong>Note :</strong> <a href="http://webaim.org/techniques/css/invisiblecontent/">Invisible Content Just for Screen Reader Users</a> vous décrira beaucoup de détails utilesà propos de ce sujet. </p>
</div>

<h3 id="JavaScript">JavaScript</h3>

<p>Le JavaScript a le même type de problèmes que le CSS concernant l'accessibilité — cela peut être désastreux pour l'accessibilité si mal utilisé, ou trop utilisé. Nous avions déjà abordé quelques problèmes d'accessibilité en rapport avec le JavaScript, principalement dans le champ de la sémantique HTML — vous devez toujours utiliser une sémantique HTML appropriée pour implémenter une fonctionnalité qu'importe où elle est disponible, par exemple utiliser des liens et des boutons de façon appropriée. N'utilisez pas les éléments <code>&lt;div&gt;</code> avec du code JavaScript pour simuler une fonctionnalité si c'est possible — c'est une source d'erreur, et ça fonctionne mieux d'utiliser les fonctionnalités disponibles qu'HTML vous fournit.</p>

<h4 id="Fonctionnalité_simple">Fonctionnalité simple</h4>

<p>Normalement, une fonctionnalité simple doit marcher uniquement avec le HTML en place — le JavaScript ne doit pas être utilisé que pour améliorer la fonctionnalité, par pour la construire en entier. Les bons usages de JavaScript incluent :</p>

<ul>
 <li>Fournir une validation de formulaire côté client, qui informe rapidement les utilisateurs des problèmes avec leurs entrées dans le formulaire, sans qu'ils aient à attendre que le serveur vérifie les données. Si ça n'est pas disponible, le formulaire marchera toujours, mais la validation sera peut-être plus lente.</li>
 <li>Fournir des contrôles personnalisés pour les <code>&lt;video&gt;</code>s HTML5 qui sont accessibles pour les utilisateurs uniquement au clavier (comme nous l'avons dit auparavant, les contrôles par défaut de navigateur ne sont pas accessibles au clavier dans la plupart des navigateurs).</li>
</ul>

<div class="note">
<p><strong>Note :</strong> <a href="http://webaim.org/techniques/javascript/">Accessible JavaScript</a> de WebAIM fourni des renseignements approfondis à propos des considérations pour du JavaScript accessible.</p>
</div>

<p>Les implémentations JavaScript plus complexes peuvent mener à des problèmes avec l'accessibilité — vous devez faire ce que vous pouvez. par exemple, cela ne serait pas raisonnable d'attendre de vous que vous fassiez un jeu complexe 3D écrit avec <a href="/fr/Apprendre/WebGL">WebGL</a> accessible à 100% pour une personne aveugle, mais vous pouvez implémenter des <a href="/fr/docs/Games/Techniques/Control_mechanisms/Desktop_with_mouse_and_keyboard">contrôles clavier</a> pour qu'il soit utilisable pour un utilisateur sans souris, et réaliser une palette de couleurs suffisamment contrastée pour être utilisable par les personnes avec des lacunes pour percevoir les couleurs.</p>

<h4 id="Fonctionnalité_complexe">Fonctionnalité complexe</h4>

<p>L'un des domaines de problématique principal pour l'accessibilité c'est les applis complexes qui nécessitent des contrôles de formulaires compliqués (comme les sélecteurs de date) et le contenu dynamique qui se met souvent à jour et de façon incrémentale.</p>

<p>Les contrôles de formulaire compliqués non natifs sont problématiques parce qu'ils ont tendance à nécessiter beaucoup de <code>&lt;div&gt;</code>s imbriquées, et le navigateur ne sait pas quoi faire par défaut avec elles. Si vous les inventer vous-même, vous devez vous assurer qu'ils sont accessibles par le clavier ; si vous utilisez des structures externes, revoyez en profondeur les options disponibles pour voir à quel point elles sont accessibles avant de vous plonger dedans. <a href="http://getbootstrap.com/">Bootstrap</a> à l'air d'être assez bon pour l'accessibilité, par exemple, bien que <a href="https://www.sitepoint.com/making-bootstrap-accessible/">Making Bootstrap a Little More Accessible</a> de Rhiana Heath aborde certain de ses problèmes (principalement en rapport avec le contraste des couleurs), et examine certaines solutions.</p>

<p>Le contenu dynamique régulièrement mis à jour peut-être un problème parce que les utilisateurs de lecteur d'écran peuvent le manquer, spécialement si les mises à jour sont inattendues. Si vous avez une appli en single-page avec un contenu principal dans un panneau qui est régulièrement mis à jour en utilisant <a href="/fr/docs/Web/API/XMLHttpRequest">XMLHttpRequest</a> ou <a href="/fr/docs/Web/API/Fetch_API">Fetch</a>, un utilisateur utilisant un lecteur d'écran peut rater ces mises à jour.</p>

<h4 id="WAI-ARIA">WAI-ARIA</h4>

<p>Avez-vous besoin d'utiliser une fonctionnalité complexe, ou à la place vous le faîte avec une bonne vieille sémantique HTML ? Si vous avez besoin de complexité, vous devriez songer à utiliser <a href="https://www.w3.org/TR/wai-aria-1.1/">WAI-ARIA</a> (Accessible Rich Internet Applications), une spécification qui fournit une sémantique (sous la forme des nouveaux attributs HTML) pour les objets comme les contrôles complexes de formulaire et les panneaux mis à jour qui peuvent être compris par la plupart des navigateurs et les lecteurs d'écran.</p>

<p>Pour traiter avec les widgets complexes de formulaire, vous devez utiliser les attributs ARIA comme <code>roles</code> pour déclarer quel rôle les différents éléments on dans un widget (par exemple, est-ce qu'ils sont un onglet, ou un panneau ?), <code>aria-disabled</code> pour dire si un contrôle est désactivé ou pas, etc.</p>

<p>Pour traiter avec les zones de contenu qui sont régulièrement mises à jour, vous pouvez utiliser l'attribut <code>aria-live</code>, qui identifie une zone mise à jour. Sa valeur indique avec quelle urgence le lecteur d'écran doit faire la lecture :</p>

<ul>
 <li><code>off</code> : Par défaut. Les mises à jour ne seront pas annoncées.</li>
 <li><code>polite</code> : Les mises à jour sont annoncées seulement si l'utilisateur est inactif.</li>
 <li><code>assertive</code> : Les mises à jour sont annoncées à l'utilisateur aussi tôt que possible.</li>
 <li><code>rude</code> : Les mises à jour sont annoncées immédiatement, même si cela interrompt l'utilisateur.</li>
</ul>

<p>Voici un exemple :</p>

<pre class="brush: html">&lt;p&gt;&lt;span id="LiveRegion1" aria-live="polite" aria-atomic="false"&gt;&lt;/span&gt;&lt;/p&gt;</pre>

<p>Vous pouvez voir un exemple en action sur l'exemple <a href="http://www.freedomscientific.com/Training/Surfs-up/AriaLiveRegions.htm">ARIA (Accessible Rich Internet Applications) Live Regions</a> de Freedom Scientific — le paragraphe surligné doit mettre à jour son contenu toutes les 10 secondes, et un lecteur d'écran doit le lire à l'utilisateur. <a href="http://www.freedomscientific.com/Training/Surfs-up/AriaLiveRegionsAtomic.htm">ARIA Live Regions - Atomic</a> apporte un autre exemple utile.</p>

<p>Nous n'avons pas de place pour couvrir WAI-ARIA en détail ici, vous pouvez en apprendre beaucoup plus à ce propos sur <a href="/fr/docs/Learn/Accessibility/WAI-ARIA_basics">WAI-ARIA basics</a>.</p>

<h2 id="Les_outils_d'accessibilité">Les outils d'accessibilité</h2>

<p>Maintenant que nous avons couvers les considérations de l'accessibilité pour les différentes technologies web, incluant quelques techniques de test (comme la navigation au clavier et le vérificateur de contraste de couleur), tournons-nous maintenant vers d'autres outils que vous pouvez utiliser pour faire des tests d'accessibilité.</p>

<h3 id="Les_outils_d'audit">Les outils d'audit</h3>

<p>Il y a plusieurs outils d'audit disponibles que vous pouvez placer sur vos pages web, lesquels les examinerons et retournerons une liste de problèmes d'accessibilité présents sur la page. A titre d'exemple :</p>

<ul>
 <li><a href="https://tenon.io">Tenon </a>: une assez bonne appli en ligne qui traverse le code à une URL fournie et qui retourne les résultats sur les erreurs d'acessibilité comprenant les indicateurs, ds erreurs spécifiques accompagnés des critères WCAG qu'elles affectent, et des suggestion de résolutions.</li>
 <li><a href="http://khan.github.io/tota11y/">tota11y</a> : Un outil d'accessibilité de la Khan Academy qui prend la forme d'une librairie JavaScript que vous attachez à votre page pour apporter plusieurs outils d'accessibilité.</li>
 <li><a href="http://wave.webaim.org/">Wave</a>: Un autre outil en ligne de test d'accessibilité qui accepte une adresse web et retourne une utile vue annotée de la page avec les problèmes d'accessibilité surlignés.</li>
</ul>

<p>Observons un exemple, en utilisant Tenon.</p>

<ol>
 <li>Aller sur la <a href="https://tenon.io">page d'accueil de Tenon</a>.</li>
 <li>Entrez l'URL de notre exemple de <a href="http://mdn.github.io/learning-area/accessibility/html/bad-semantics.html">bad-semantics.html</a> dans l'entrée texte en haut de la page (ou l'URL d'une autre page que vous aimeriez analyser) et appuyez sur <em>Analyse your Webpage</em>.</li>
 <li>Défilez vers le bas jusqu'à que vous trouviez la section d'erreur/signalement, comme montré ci-dessous.</li>
</ol>

<p><img alt="" src="tenon-screenshot.png"></p>

<p>Il y a également des options que vous pouvez examiner (voir le lien <em>Show Options</em> vers le haut de la page), ainsi qu'une API pour utiliser Tenon comme un programme.</p>

<div class="note">
<p><strong>Note :</strong> De tels outils ne sont pas suffisant pour résoudre tous vos problèmes d'accessibilité en tant que tel. Vous devrez les combiner, savoir et expérience, test utilisateur, etc. pour vous faire une image exacte.</p>
</div>

<h3 id="Les_outils_d'automatisation">Les outils d'automatisation</h3>

<p><a href="https://www.deque.com/products/axe/">Deque's aXe tool</a> va un peu plus loin que les outils d'audit que nous avons mentionné plus haut. Comme les autres, il vérifie les pages et retourne des erreurs d'accessibilité. Sa forme immédiate la plus utile est sûrement son extension navigateur :</p>

<ul>
 <li><a href="http://bitly.com/aXe-Chrome">aXe pour Chrome</a></li>
 <li><a href="http://bit.ly/aXe-Firefox">aXe pour Firefox</a></li>
</ul>

<p>Cela ajoute un onglet accessibilité aux outils de développeur du navigateur, nous avons installé la version pour Firefox, puis nous l'avons utilisé pour auditer notre exemple <a href="http://mdn.github.io/learning-area/accessibility/html/bad-table.html">bad-table.html</a>. Nous obtenons les résultats suivants :</p>

<p><img alt="" src="aXe-screenshot.png"></p>

<p>aXe est également installable en utilisant <code>npm</code>, et peut-être intégré avec des exécuteurs de tâche comme <a href="http://gruntjs.com/">Grunt</a> et <a href="http://gulpjs.com/">Gulp</a>, des frameworks d'automatisation comme <a href="http://www.seleniumhq.org/">Selenium</a> et <a href="https://cucumber.io/">Cucumber</a>, des framework de test unitaire comme <a href="http://jasmine.github.io/">Jasmin</a>, et d'autres encore (une fois encore, voir la <a href="https://www.deque.com/products/axe/">page principale d'aXe</a> pour plus de détails).</p>

<h3 id="Les_lecteurs_d'écran">Les lecteurs d'écran</h3>

<p>Il faut définitivement tester avec un lecteur d'écran pour s'habituer à comment les personnes malvoyantes utilisent le Web. Il y a plusieurs lecteurs d'écran disponible : </p>

<ul>
 <li>Certain sont des produits commerciaux payants, comme <a href="http://www.freedomscientific.com/Products/Blindness/JAWS">JAWS</a> (Windows) et <a href="http://www.gwmicro.com/window-eyes/">Window Eyes</a> (Windows).</li>
 <li>Certains sont des produits gratuits, comme <a href="http://www.nvaccess.org/">NVDA</a> (Windows), <a href="http://www.chromevox.com/">ChromeVox</a> (Chrome, Windows, et Mac OS X), et <a href="https://wiki.gnome.org/Projects/Orca">Orca</a> (Linux).</li>
 <li>Certains sont compris dans le système d'exploitation, comme like <a href="http://www.apple.com/accessibility/osx/voiceover/">VoiceOver</a> (Mac OS X et iOS), <a href="http://www.chromevox.com/">ChromeVox</a> (sur les Chromebooks), et <a href="https://play.google.com/store/apps/details?id=com.google.android.marvin.talkback">TalkBack</a> (Android).</li>
</ul>

<p>La plupart du temps, les lecteurs d'écran sont des applis séparées, qui s'exécutent sur le système d'exploitation hôte et peuvent lire des pages web, mais aussi du texte dans d'autres appli. Ce n'est pas toujours le cas (ChromeVox est une extension navigateur), mais ça l'est souvent. Les lecteurs d'écran ont tendance à agir de manière légèrement différente et ont des contrôles différents, donc vous devrez consulter la documentation pour le lecteur d'écran que vous avez choisi pour obtenir tous les détails — cela dit, il fonctionne tous à peu près de la même manière.</p>

<p>Commençons à effectuer quelques tests avec deux lecteurs d'écran différents pour vous donner une idée générale de comment ils fonctionnent et de comment tester avec eux.</p>

<div class="note">
<p><strong>Note :</strong> <a href="http://webaim.org/techniques/screenreader/">Designing for Screen Reader Compatibility</a> de WebAIM fournit des informations utiles à propos de l'utilisation des lecteurs d'écran et qu'est-ce qui est le plus efficace pour les lecteurs d'écran. Aller également voir <a href="http://webaim.org/projects/screenreadersurvey6/#used">Screen Reader User Survey #6 Results</a> pour des statistiques intéressantes concernant l'utilisation de lecteur d'écran.</p>
</div>

<h4 id="VoiceOver">VoiceOver</h4>

<p>VoiceOver (VO) est gratuit avec votre Mac/iPhone/iPad, donc c'est utile pour tester sur votre ordinateur/mobile si vous utilisez des produits Apple. Nous le testerons sur Mac OS X sur un MacBook Pro.</p>

<p>Pour le démarrer, pressez Cmd + Fn + F5. Si vous n'avez jamais utilisé VO auparavant, vous obtiendrez un écran de bienvenue où vous pouvez choisir de démarrer VO ou de ne pas le démarrer, et vous parcourrez un tutoriel utile pour apprendre à comment l'utiliser. Pour l'arrêter, pressez Cmd + Fn + F5 à nouveau.</p>

<div class="note">
<p><strong>Note :</strong> Vous devriez parcourir le tutoriel au moins une fois — il est vraiment très utile pour en apprendre à propos de VO.</p>
</div>

<p>Lorsque VO est démarré, l'affichage ressemblera à peu près à cela, mais vous verrez une boîte noire en bas à gauche de l'écran qui contient l'information sur quoi est-ce que VO est actuellement sélectionné. La sélection courante sera également mise en avant, avec une bordure noire — cette mise en avant est connue comme le <strong>curseur VO</strong>.</p>

<p><img alt="" src="voiceover.png"></p>

<p>Pour utiliser VO, vous aller beaucoup utiliser le "modificateur VO" — c'est une touche ou une combinaison de touches que vous devez presser en plus de l'actuel raccourci VO pour qu'elles fonctionnent. Utiliser un modificateur comme celui-ci est courant avec les lecteurs d'écran, pour leur permettre de garder leur propres commandes en évitant d'entrer en conflit avec d'autres commandes. Dans le cas de VO, le modificateur peut aussi être VerrMaj, ou Ctrl + Option.</p>

<p>VO a beaucoup de commandes clavier, et nous n'allons pas toutes les lister ici. Les principales dont vous aurez besoin pour tester une page web sont dans le tableau suivant. Dans les raccourcis clavier, "VO" veut dire "le modificateur VoiceOver".</p>

<table class="standard-table">
 <caption>
 <p>Les raccourcis clavier VoiceOver les plus communs</p>
 </caption>
 <thead>
  <tr>
   <th scope="col">Raccourci clavier</th>
   <th scope="col">Description</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>VO + Touches du curseur</td>
   <td>Déplace le curseur VO vers le haut, la droite, le bas, la gauche.</td>
  </tr>
  <tr>
   <td>VO + Barre espace</td>
   <td>
    <p>Sélectionne/active les éléments mis en avant par le curseur VO. Cela inclut les items sélectionnés dans le Rotor (voir plus bas).</p>
   </td>
  </tr>
  <tr>
   <td>VO + Shift + curseur bas</td>
   <td>
    <p>Se déplacer dans un groupe d'éléments (comme un tableau HTML, ou un formulaire, etc.) Une fois dans un groupe vous pouvez vous déplacer et sélectionner les éléments à l'intérieur de ce groupe en utilisant les commandes ci-dessus normalement.</p>
   </td>
  </tr>
  <tr>
   <td>VO + Shift + curseur haut</td>
   <td>Sortir d'un groupe.</td>
  </tr>
  <tr>
   <td>VO + C</td>
   <td>
    <p>(à l'intérieur d'un tableau) lire l'entête de la colonne courante.</p>
   </td>
  </tr>
  <tr>
   <td>VO + R</td>
   <td>(à l'intérieur d'un tableau) lire l'entête de la ligne courante.</td>
  </tr>
  <tr>
   <td>VO + C + C (deux C d'affilé)</td>
   <td>(à l'intérieur d'un tableau) lire toute la colonne courante, incluant l'entête.</td>
  </tr>
  <tr>
   <td>VO + R + R (deux R d'affilé)</td>
   <td>
    <p>(à l'intérieur d'un tableau) lire toute la ligne courante, incluant les entêtes qui correspondent à chacune des cellules.</p>
   </td>
  </tr>
  <tr>
   <td>VO + curseur gauche, VO + curseur droit</td>
   <td>(à l'intérieur d'options horizontales, comme un sélecteur de date ou de temps) Se déplacer entre les options</td>
  </tr>
  <tr>
   <td>VO + curseur haut, VO + curseur bas</td>
   <td>(à l'intérieur d'options horizontales, comme un sélecteur de date ou de temps) Modifier l'option courante.</td>
  </tr>
  <tr>
   <td>VO + U</td>
   <td>
    <p>Utiliser le rotor, qui affiche des listes de rubriques, de liens, de contrôles de formulaires, etc. pour une navigation simplifiée.</p>
   </td>
  </tr>
  <tr>
   <td>VO + curseur gauche, VO + curseur droit</td>
   <td>
    <p>(à l'intérieur du Rotor) Se déplacer ente les différentes listes disponibles dans le Rotor.</p>
   </td>
  </tr>
  <tr>
   <td>VO + curseur haut, VO + curseur bas</td>
   <td>
    <p>(à l'intérieur du Rotor) Se déplacer entre les différents éléments dans la liste courante du Rotor.</p>
   </td>
  </tr>
  <tr>
   <td>Esc</td>
   <td>(à l'intérieur du Rotor) Sortir du Rotor.</td>
  </tr>
  <tr>
   <td>Ctrl</td>
   <td>(Lorsque VO parle) Arrêter/Reprendre l'allocution.</td>
  </tr>
  <tr>
   <td>VO + Z</td>
   <td>Relance la dernière partie de l'allocution.</td>
  </tr>
  <tr>
   <td>VO + D</td>
   <td>
    <p>Aller dans le Dock du Mac, pour que vous puissiez sélectionner des applis à exécuter.</p>
   </td>
  </tr>
 </tbody>
</table>

<p>Cela peut paraître comme beaucoup de commandes, mais pas tant que ça que vous vous y habituez, et VO vous rappelle régulièrement quels commandes utiliser dans quels cas. Essayer de tester VO maintenant ; vous pouvez dorénavant essayer de tester certains de nos exemples dans la section {{anch("Screenreader testing")}}.</p>

<h4 id="NVDA">NVDA</h4>

<p>NVDA est exclusif à Windows, et vous allez devoir l'installer.</p>

<ol>
 <li>Téléchargez-le depuis <a href="http://www.nvaccess.org/">nvaccess.org</a>. Vous pouvez choisir si vous voulez faire une donation ou le télécharger gratuitement ; vous devrez également leur donner votre adresse e-mail avant de pouvoir le télécharger.</li>
 <li>Une fois téléchargé, installez-le — double cliquez sur l'installeur, acceptez la licence et suivez les instructions.</li>
 <li>Pour lancer NVDA, double cliquez sur fichier/raccourci du programme, ou utilisez le raccourci clavier Ctrl + Alt + N. Vous verrez la boîte de dialogue de bienvenue de NVDA lorsque vous le démarrez. Vous pouvez choisir ici différentes options, puis appuyez sur <em>OK</em> pour continuer.</li>
</ol>

<p>NVDA sera maintenant actif sur votre ordinateur.</p>

<p>Pour utiliser NVDA, vous aller beaucoup utiliser le "modificateur NVDA" — c'est une touche que vous devez presser en plus de l'actuel raccourci NVDA pour qu'elles fonctionnent. Utiliser un modificateur comme celui-ci est courant avec les lecteurs d'écran, pour leur permettre de garder leurs propres commandes en évitant d'entrer en conflit avec d'autres commandes. Dans le cas de NVDA, le modificateur peut aussi être Insert (par défaut), ou VerrMaj (peut être choisi en cochant la première case à cocher dans la boîte de dialogue de bienvenue avant d'appuyer sur <em>OK</em>).</p>

<div class="note">
<p><strong>Note :</strong> NVDA est plus subtile que VoiceOver en termes de comment il met en valeur là où il est et qu'est-ce qu'il fait. Lorsque vous défilez à travers des rubriques, listes, etc. les éléments que vous sélectionnez seront généralement mis à avant avec un contour subtile, mais ça n'est pas toujours le cas pour toutes les choses. Si vous vous retrouvez complètement perdu, vous pouvez appuyer sur Ctrl + F5 pour rafraîchir la page courante et recommencer en haut de la page.</p>
</div>

<p>NVDA a beaucoup de commandes clavier, et nous n'allons pas toutes les lister ici. Les principales dont vous aurez besoin pour tester une page web sont dans le tableau suivant. Dans les raccourcis clavier, "NVDA" veut dire "le modificateur NVDA".</p>

<table class="standard-table">
 <caption>Les raccourcis clavier NVDA les plus communs</caption>
 <thead>
  <tr>
   <th scope="col">Raccourci clavier</th>
   <th scope="col">Description</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>NVDA + Q</td>
   <td>
    <p>Arrête NVDA après que vous l'ayez démarré.</p>
   </td>
  </tr>
  <tr>
   <td>NVDA + curseur haut</td>
   <td>Lit la ligne courante.</td>
  </tr>
  <tr>
   <td>NVDA + curseur bas</td>
   <td>Commence à lire à la position courante.</td>
  </tr>
  <tr>
   <td>curseur haut ou curseur bas, ou Shift + Tab et Tab</td>
   <td>
    <p>Se déplace à l'élément suivant/précédent de la page et le lit.</p>
   </td>
  </tr>
  <tr>
   <td>curseur gauche et curseur droit</td>
   <td>
    <p>Se déplace au caractère suivant/précédent dans l'élément courant et le lit.</p>
   </td>
  </tr>
  <tr>
   <td>Shift + H et H</td>
   <td>
    <p>Se déplace au titre suivante/précédente et le lit.</p>
   </td>
  </tr>
  <tr>
   <td>Shift + K et K</td>
   <td>
    <p>Se déplace au lien suivant/précédent et le lit.</p>
   </td>
  </tr>
  <tr>
   <td>Shift + D et D</td>
   <td>
    <p>Se déplace au repère de document (par ex. <code>&lt;nav&gt;</code>) suivant/précédent et le lit.</p>
   </td>
  </tr>
  <tr>
   <td>Shift + 1–6 et 1–6</td>
   <td>
    <p>Se déplace au titre (niveau 1 à 6) suivant/précédent et le lit.</p>
   </td>
  </tr>
  <tr>
   <td>Shift + F et F</td>
   <td>
    <p>Se déplace à l'entrée de formulaire suivante/précédente et se focalise dessus.</p>
   </td>
  </tr>
  <tr>
   <td>Shift + T et T</td>
   <td>
    <p>Se déplace sur la donnée de tableau suivante/précédente et se focalise dessus.</p>
   </td>
  </tr>
  <tr>
   <td>Shift + B et B</td>
   <td>
    <p>Se déplace sur le bouton suivant/précédent et lit son libellé.</p>
   </td>
  </tr>
  <tr>
   <td>Shift + L et L</td>
   <td>
    <p>Se déplace à la liste suivante/précédente et lit son premier item de liste.</p>
   </td>
  </tr>
  <tr>
   <td>Shift + I et I</td>
   <td>
    <p>Se déplace à l'item de liste suivant/précédent et le lit.</p>
   </td>
  </tr>
  <tr>
   <td>Entrée/Retour</td>
   <td>
    <p>(quand un lien/bouton ou autre élément activable est sélectionné) Active l'élément.</p>
   </td>
  </tr>
  <tr>
   <td>NVDA + Barre espace</td>
   <td>
    <p>(quand un formulaire est sélectionné) Entre dans le formulaire pour que les éléments puissent être sélectionnés individuellement, ou quitter le formulaire si vous êtes déjà dedans.</p>
   </td>
  </tr>
  <tr>
   <td>Shift Tab et Tab</td>
   <td>
    <p>(à l'intérieur d'un formulaire) Se déplacer entre les entrées de formulaire.</p>
   </td>
  </tr>
  <tr>
   <td>Curseur haut et curseur bas</td>
   <td>
    <p>(à l'intérieur d'un formulaire) Modifier les valeurs d'une entrée de formulaire (dans les cas comme les listes déroulantes)</p>
   </td>
  </tr>
  <tr>
   <td>Barre espace</td>
   <td>
    <p>(à l'intérieur d'un formulaire) Sélectionner la valeur choisie.</p>
   </td>
  </tr>
  <tr>
   <td>Ctrl + Alt + touches fléchées</td>
   <td>(à l'intérieur d'un tableau) Se déplacer entre les cellules du tableau.</td>
  </tr>
 </tbody>
</table>

<h4 id="Test_avec_lecteur_d'écran">Test avec lecteur d'écran</h4>

<p>Maintenant que vous vous êtes habitué à utiliser un lecteur d'écran, nous aimerions que vous vous habituiez à faire quelques tests d'accessibilité rapides, pour vous faire une idée de comment les lecteurs d'écran se débrouillent avec les bonnes et mauvaises caractéristiques d'une page web :</p>

<ul>
 <li>Regardez <a href="http://mdn.github.io/learning-area/accessibility/html/good-semantics.html">good-semantics.html</a>, et notez comment les titres sont trouvés pas le lecteur d'écran et rendus disponibles pour être utilisés en navigation. Regardez maintenant <a href="http://mdn.github.io/learning-area/accessibility/html/bad-semantics.html">bad-semantics.html</a>, et observez comme le lecteur d'écran n'obtient aucune de ces informations. Imaginez à quel point cela peut être pénible lorsque vous essayez de naviguer sur une page de texte vraiment longue.</li>
 <li>Regardez <a href="http://mdn.github.io/learning-area/accessibility/html/good-links.html">good-links.html</a>, et notez comment est-ce qu'ils ont du sens vus hors contexte. Ce n'est pas le cas avec <a href="http://mdn.github.io/learning-area/accessibility/html/bad-links.html">bad-links.html</a> — ceux sont juste tous des "click here".</li>
 <li>Regardez <a href="http://mdn.github.io/learning-area/accessibility/html/good-form.html">good-form.html</a>, et regardez comment les entrées du formulaire sont décrites en utilisant leurs libellés parce que nous avons utilisé l'élément <code>&lt;label&gt;</code> correctement. Dans <a href="http://mdn.github.io/learning-area/accessibility/html/bad-form.html">bad-form.html</a>, ils ne sont que des "blank" sur toute la ligne, totalement inutiles.</li>
 <li>Regardez notre exemple <a href="http://mdn.github.io/learning-area/css/styling-boxes/styling-tables/punk-bands-complete.html">punk-bands-complete.html</a>, et observez comment le lecteur d'écran est capable d'associer les colonnes et les lignes de contenu et de les lires toutes ensembles, parce que nous avons défini les entêtes correctement. Dans <a href="http://mdn.github.io/learning-area/accessibility/html/bad-table.html">bad-table.html</a>, aucune des cellules ne peut être associée du tout. Notez que NVDA a étonnamment l'air d'assez bien se comporter lorsque vous n'avez qu'un seul tableau sur une page ; à la place vous pouvez essayer <a href="http://webaim.org/articles/nvda/tables.htm">WebAIM's table test page</a>.</li>
 <li>Jetez un œil à <a href="http://www.freedomscientific.com/Training/Surfs-up/AriaLiveRegions.htm">WAI-ARIA live regions example</a> que nous avons vu plus tôt, et observez comment le lecteur d'écran va continuer de lire la section qui se met à constamment à jour dès qu'elle se met à jour.</li>
</ul>

<h3 id="Test_utilisateur">Test utilisateur</h3>

<p>Comme mentionné plus haut, vous ne pouvez pas uniquement compter sur les outils automatisés pour déterminer les problèmes d'accessibilité sur votre site. Il est recommandé que lorsque vous établissez votre plan de test, vous devez inclure quelques groupes d'utilisateur d'accessibilité si c'est possible (voir notre section <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Testing_strategies#Les_tests_utilisateurs">Test Utilisateur</a> plus tôt dans ce cours pour plus de contexte). Essayez d'inclure des utilisateurs de lecteur d'écran, des utilisateurs exclusifs au clavier, des utilisateurs malentendants, et peut-être d'autres groupes encore, selon vos besoins.</p>

<h2 id="Checklist_de_tests_d'accessibilité">Checklist de tests d'accessibilité</h2>

<p>La liste suivante vous fournit une checklist à suivre pour vous assurer de mener à bien les tests d'accessibilité recommandés pour votre projet :</p>

<ol>
 <li>Assurez-vous que votre HTML est sémantiquement correct au possible. <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/HTML_et_CSS#La_validation">Le valider</a> est un bon début, comme utiliser un <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility#Auditing_tools">outil d'Audit</a>.</li>
 <li>Vérifiez que votre contenu a du sens lorsque le CSS est désactivé.</li>
 <li>Assurez-vous que votre fonctionnalité est <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility#Using_native_keyboard_accessibility">accessible au clavier</a>. Testez en utilisant Tab, Retour/Entrée, etc.</li>
 <li>Assurez-vous que votre contenu non-textuel a un <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility#Text_alternatives">texte alternatif</a>. Un <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility#Auditing_tools">Outil d'audit</a> est bien pour repérer ce type de problèmes.</li>
 <li>Assurez-vous que votre <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility#Color_and_color_contrast">contraste de couleurs</a> est acceptable, en utilisant un outil de vérification approprié.</li>
 <li>Assurez-vous que le <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility#Hiding_content">contenu caché</a> est visible par les lecteurs d'écran.</li>
 <li>Assurez-vous qu'une fonctionnalité est utilisable sans JavaScript autant que possible.</li>
 <li>Utilisez ARIA pour améliorer l'accessibilité quand c'est approprié.</li>
 <li>Exécutez votre site dans un <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility#Auditing_tools">Outil d'audit</a>.</li>
 <li>Testez avec un lecteur d'écran.</li>
 <li>Incluez une politique/déclaration d'accessibilité à un endroit que l'on peut trouver sur votre site pour dire ce que vous avez fait.</li>
</ol>

<h2 id="Trouver_de_l'aide">Trouver de l'aide</h2>

<p>Il y a bien d'autres problèmes que vous allez rencontrer avec l'accessibilité ; la chose la plus importante à vraiment savoir est comment trouver des réponses en ligne. Consultez l'article <a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/HTML_et_CSS#Trouver_de_l'aide">la section Trouver de l'aide</a> de l'article sur le HTML et le CSS pour des bonnes directions.</p>

<h2 id="Résumé">Résumé</h2>

<p>Espérons que cet article vous aura donné des bonnes connaissances concernant les problèmes principaux d'accessibilité que vous pourrez rencontrer, et comment les tester et les surmonter.</p>

<p>Dans le prochain article nous nous tournerons vers la fonctionnalité de détection dans plus de détail.</p>

<p>{{PreviousMenuNext("Learn/Tools_and_testing/Cross_browser_testing/JavaScript","Learn/Tools_and_testing/Cross_browser_testing/Feature_detection", "Learn/Tools_and_testing/Cross_browser_testing")}}</p>

<p> </p>

<h2 id="Dans_ce_module">Dans ce module</h2>

<ul>
 <li><a href="/fr/docs/">Introduction au test en navigateur croisé</a></li>
 <li><a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Testing_strategies">Stratégies pour mener à bien vos tests</a></li>
 <li><a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/HTML_et_CSS">Gérer les problèmes courants en HTML et CSS</a></li>
 <li><a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/JavaScript">Gérer les problèmes courants en JavaScript</a></li>
 <li><a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility">Handling common accessibility problems</a></li>
 <li><a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Feature_detection">Implementing feature detection</a></li>
 <li><a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Automated_testing">Introduction to automated testing</a></li>
 <li><a href="/fr/docs/Learn/Tools_and_testing/Cross_browser_testing/Your_own_automation_environment">Setting up your own test automation environment</a></li>
</ul>

<p> </p>