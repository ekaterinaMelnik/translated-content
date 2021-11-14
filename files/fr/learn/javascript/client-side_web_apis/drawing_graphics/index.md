---
title: Dessiner des éléments graphiques
slug: Learn/JavaScript/Client-side_web_APIs/Drawing_graphics
tags:
  - API
  - Apprendre
  - Articles
  - Canvas
  - Codage
  - Débutant
  - Graphismes
  - JavaScript
  - WebGL
translation_of: Learn/JavaScript/Client-side_web_APIs/Drawing_graphics
original_slug: Apprendre/JavaScript/Client-side_web_APIs/Drawing_graphics
---
<div>{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/Client-side_web_APIs/Third_party_APIs", "Learn/JavaScript/Client-side_web_APIs/Video_and_audio_APIs", "Learn/JavaScript/Client-side_web_APIs")}}</div>

<p>Le navigateur contient des outils de programmation graphique très puissants, du langage <a href="/fr/docs/Web/SVG">SVG</a> (Scalable Vector Graphics), aux APIs pour dessiner sur les éléments HTML {{htmlelement("canvas")}}, (voir <a href="/fr/docs/Web/HTML/Canvas">API Canvas</a> et <a href="/fr/docs/Web/API/WebGL_API">WebGL</a>). Cet article fournit une introduction à canvas et introduit d'autres ressources pour vous permettre d'en apprendre plus.</p>

<table class="standard-table">
 <tbody>
  <tr>
   <th scope="row">Prérequis:</th>
   <td>Bases de JavaScript (voir <a href="/fr/docs/Learn/JavaScript/First_steps">premiers pas</a>, <a href="/fr/Apprendre/JavaScript/Building_blocks">les briques JavaScript</a>, <a href="/fr/docs/Learn/JavaScript/Objects">introduction aux objets</a>), les <a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Introduction">notions de bases des APIs côté client</a></td>
  </tr>
  <tr>
   <th scope="row">Objectif:</th>
   <td>Apprendre les bases pour dessiner sur des éléments <code>&lt;canvas&gt;</code> en utilisant JavaScript.</td>
  </tr>
 </tbody>
</table>

<h2 id="Éléments_graphiques_sur_le_Web">Éléments graphiques sur le Web</h2>

<p>Comme nous en avons parlé dans notre module HTML <a href="/fr/Apprendre/HTML/Multimedia_and_embedding">Multimédia et Intégration</a>, le web était à l'origine uniquement du texte, ce qui était très ennuyeux. Les images ont donc été introduites — d'abord via l'élément {{htmlelement("img")}} et plus tard via les propriétés CSS comme {{cssxref("background-image")}}, et <a href="/fr/docs/Web/SVG">SVG</a>.</p>

<p>Ce n'était cependant toujours pas assez. Tandis qu'il était possible d'utiliser <a href="/fr/Apprendre/CSS">CSS</a> et <a href="/fr/Apprendre/JavaScript">JavaScript</a> pour animer (ou manipuler) les images vectorielles SVG — puisqu'elles sont définies par le balisage — il n'y avait aucun moyen de faire de même pour les images bitmap, et les outils disponibles étaient plutôt limités. Le Web n'avait toujours pas de moyen efficace de créer des animations de jeux, des scènes 3D, et autres dispositions couramment traitées par les langages de bas niveau tels que C++ ou Java.</p>

<p>La situation a commencé à s'améliorer quand les navigateurs ont commencé à prendre en charge l'élément {{htmlelement("canvas")}} et l' <a href="/fr/docs/Web/HTML/Canvas">API Canvas</a> associée — Apple l'a inventée vers 2004, et les autres navigateurs l'ont l'implémentée dans les années qui ont suivi. Comme vous le verrez dans cet article, canvas fournit de nombreux outils utiles à la création d'animation 2D, jeux, visualisations de données, et autres types d'application, particulièrement quand il est combiné à d'autres APIs que la plateforme web fournit.</p>

<p>L'exemple ci-dessous montre une simple animation de balles qui rebondissent en canvas 2D, que nous avons déjà vue dans notre module <a href="/fr/docs/Learn/JavaScript/Objects/la_construction_d_objet_en_pratique">La construction d'objet en pratique</a>:</p>

<p>{{EmbedGHLiveSample("learning-area/javascript/oojs/bouncing-balls/index-finished.html", '100%', 500)}}</p>

<p>Autour de 2006-2007, Mozilla a commencé à travailler sur une implémentation expérimentale de canvas 3D. C'est devenu <a href="/fr/Apprendre/WebGL">WebGL</a>, lequel a gagné en popularité parmi les fournisseurs de navigateur, et a été standardisé autour de 2009-2010. WebGL permet de créer de véritables graphiques 3D dans le navigateur web; l'exemple ci-dessous montre un simple cube WebGL qui tourne:</p>

<p>{{EmbedGHLiveSample("learning-area/javascript/apis/drawing-graphics/threejs-cube/index.html", '100%', 500)}}</p>

<p>Cet article se concentrera principalement sur les canvas 2D, car le code WebGL brut est très complexe. Nous montrerons cependant comment utiliser une bibliothèque WebGL pour créer une scène 3D plus facilement, et vous pourrez  par la suite suivre le tutoriel <a href="/fr/Apprendre/WebGL">WebGL</a>, qui couvre le code WebGL brut.</p>

<div class="note">
<p><strong>Note :</strong> Canvas est très bien pris en charge parmi les différents navigateurs, à l'exception de IE 8 (et inférieur) pour les canvas 2D, et IE 11 (et inférieur) pour WebGL.</p>
</div>

<h2 id="Apprentissage_actif_Débuter_avec_un_&lt;canvas>">Apprentissage actif: Débuter avec un &lt;canvas&gt;</h2>

<p>Si vous voulez créer une scène 2D ou 3D sur une page web, vous devez commencer avec un élément HTML {{htmlelement("canvas")}}. Cet élément est utilisé pour définir la zone de la page où l'image sera dessinée. C'est aussi simple que d'inclure l'élément dans la page:</p>

<pre class="brush: html">&lt;canvas width="320" height="240"&gt;&lt;/canvas&gt;</pre>

<p>Cela va créer un canvas sur la page d'une taille de 320 pixels par 240.</p>

<p>À l'intérieur des balises du canvas, vous pouvez mettre du contenu alternatif, qui est affiché si le navigateur de l'utilisateur ne prend pas en charge les canvas.</p>

<pre class="brush: html">&lt;canvas width="320" height="240"&gt;
  &lt;p&gt;Votre navigateur ne prend pas en charge canvas. Boo hoo!&lt;/p&gt;
&lt;/canvas&gt;</pre>

<p>Bien sûr, le message ci-dessus est vraiment inutile! Dans un exemple réel, vous voudriez plutôt associer le contenu alternatif au contenu du canvas. Par exemple, si vous voulez afficher un graphique en temps réel des cours boursiers, le contenu alternatif pourrait être une image statique du dernier graphique, avec un texte indiquant quels sont les prix.</p>

<h3 id="Crée_et_dimensionner_notre_canvas">Crée et dimensionner notre canvas</h3>

<p>Commençons par créer notre propre canvas, que nous utiliserons pour dessiner nos futures expériences.</p>

<ol>
 <li>
  <p>Premièrement, copiez localement notre fichier <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/0_canvas_start.html">0_canvas_start.html</a>, et ouvez-le dans votre éditeur de texte.</p>
 </li>
 <li>
  <p>Ajoutez le code suivant à l'intérieur, juste après la balise {{htmlelement("body")}} ouvrante:</p>

  <pre class="brush: html">&lt;canvas class="myCanvas"&gt;
  &lt;p&gt;Ajouter un contenu alternatif approprié ici.&lt;/p&gt;
&lt;/canvas&gt;</pre>

  <p>Nous avons ajouté un attribut <code>class</code> à l'élément <code>&lt;canvas&gt;</code> pour que ce soit plus facile à sélectionner dans le cas où nous aurions plusieurs canvas sur la page. Et nous avons supprimé les attributs <code>width</code> et <code>height</code> pour le moment (vous pouvez les remettre si vous le voulez mais nous les définirons en utilisant JavaScript dans une section plus bas). Les canvas sans hauteur et largeur explicites sont définits par défaut à 300 pixels par 150.</p>
 </li>
 <li>
  <p>Maintenant, ajoutez les lignes suivantes à l'intérieur de l'élément {{htmlelement("script")}}:</p>

  <pre class="brush: js">var canvas = document.querySelector('.myCanvas');
var width = canvas.width = window.innerWidth;
var height = canvas.height = window.innerHeight;</pre>

  <p>Ici, nous avons stocké une référence vers le canvas dans la variable <code>canvas</code>. Sur la deuxième ligne, nous affectons à la fois une nouvelle variable <code>width</code> et la propriété <code>width</code> du canvas à {{domxref("Window.innerWidth")}} (ce qui nous donne la largeur de la fenêtre). Sur la troisième ligne, nos affectons à la fois une nouvelle variable <code>height</code> et la propriété <code>height</code> du canvas à {{domxref("Window.innerHeight")}} (ce qui nous donne la hauteur de la fenêtre). Nous avons donc un canvas qui remplit toute la largeur et hauteur de la fenêtre!</p>

  <p>Vous avez également vu que nous avons chaîné les assignations ensemble avec plusieurs signes égal — ce qui est autorié en JavaScript, et c'est une bonne technique si vous voulez que plusieurs variables aient la même valeur. Nous avons gardé la hauteur et largeur du canvas facilement accessibles dans les variables width/height, ces valeurs seront utiles plus tard (par exemple, si vous voulez dessiner quelque chose exactement à mi-chemin de la largeur du canvas).</p>
 </li>
 <li>
  <p>Si vous sauvegardez et chargez votre exemple dans le navigateur maintenant, vous ne verrez rien, ce qui est normal, mais vous verrez également des barres de défilement, ce qui est un problème pour nous. Cela se produit parce que l'élément {{htmlelement("body")}} a des {{cssxref("margin")}} qui, ajoutées à la taille du canvas, résulte en un document qui est plus large que la fenêtre. Pour se débarasser des barres de défilement, nous devons supprimer les {{cssxref("margin")}} et aussi définir {{cssxref("overflow")}} à <code>hidden</code>. Ajoutez ce qui suit à l'intérieur du {{htmlelement("head")}} du document:</p>

  <pre class="brush: html">&lt;style&gt;
  body {
    margin: 0;
    overflow: hidden;
  }
&lt;/style&gt;</pre>

  <p>Les barres de défilement ne devraient plus être là.</p>
 </li>
</ol>

<div class="note">
<p><strong>Note :</strong> Vous devrez généralement définir la taille de l'image en utilisant les attributs HTML ou les propriétéss DOM, comme expliqué ci-dessus. Vous pourriez théoriquement utiliser CSS, le problème étant que le dimensionnement le canvas est alors effectué après que le contenu canvas n'ait été calculé, et comme toute autre image (puisque le canvas une fois affiché n'est plus qu'une simple image), elle peut devenir pixelisée/déformée.</p>
</div>

<h3 id="Obtenir_le_contexte_du_canvas_et_configuration_finale">Obtenir le contexte du canvas et configuration finale</h3>

<p>Nous devons faire une dernière chose avant de considérer notre template finit. Pour dessiner sur le canvas, nous devons récupérer une référence à la zone de dessin, appelé un <em>contexte</em>. Pour ce faire, on utilise la méthode {{domxref("HTMLCanvasElement.getContext()")}}, qui, pour un usage basique ne prend qu'un seul paramètre, spécifiant quel type de contexte nous voulons récupérer.</p>

<p>En l'occurence, nous voulons un canvas 2D, alors ajoutez le JavaScript suivant à la suite des autres instructions à l'intérieur de l'élément <code>&lt;script&gt;</code>:</p>

<pre class="brush: js">var ctx = canvas.getContext('2d');</pre>

<div class="note">
<p><strong>Note :</strong> Vous pouvez choisir d'autres types de contexte comme <code>webgl</code> pour WebGL, <code>webgl2</code> pour WebGL 2, etc., mais nous n'en aurons pas besoin dans cet article.</p>
</div>

<p>Voilà — notre canvas est maintenant préparé et prêt à être dessiné! La variable <code>ctx</code> contient désormais un objet {{domxref("CanvasRenderingContext2D")}}, et toutes les opérations de dessin sur le canvas impliqueront de manipuler cet objet.</p>

<p>Faisons une dernière chose avant de passer à autre chose. Nous allons colorier l'arrière-plan du canvas en noir, cela vous donnera un avant-goût de l'API canvas. Ajoutez les lignes suivantes au bas de votre JavaScript:</p>

<pre class="brush: js">ctx.fillStyle = 'rgb(0, 0, 0)';
ctx.fillRect(0, 0, width, height);</pre>

<p>Ici nous définissons une couleur de remplissage en utilisant la propriété du canvas {{domxref("CanvasRenderingContext2D.fillStyle", "fillStyle")}} (qui prend une <a href="/fr/Apprendre/CSS/Introduction_à_CSS/Values_and_units#Couleurs">valeur de couleur</a> tout comme les propriétés CSS), puis nous dessinons un rectangle qui recouvre intégralement la surface du canvas avec la méthode {{domxref("CanvasRenderingContext2D.fillRect", "fillRect")}} (les deux premiers paramètres sont les coordonnées du coin supérieur gauche du rectangle; les deux derniers sont la largeur et la hauteur du rectangle que vous voulez dessiner — on vous avait dit que ces variables <code>width</code> et <code>height</code> allaient être utiles)!</p>

<p>OK, notre template est prêt et il est temps de passer à autre chose.</p>

<h2 id="Les_bases_du_canvas_2D">Les bases du canvas 2D</h2>

<p>Pour rappel, toutes les opération de dessin sont effectuées en manipulant un objet {{domxref("CanvasRenderingContext2D")}} (dans notre cas, <code>ctx</code>).</p>

<p>De nombreuses opérations doivent recevoir des coordonnées en entrée pour savoir où dessiner quelque chose — le coin supérieur gauche du canvas est le point (0, 0), l'axe horizontal (x) va de gauche à droite, et l'axe vertical (y) va de haut en bas.</p>

<p><img alt="" src="Canvas_default_grid.png"></p>

<p>Dessiner des formes est souvent fait en utilisant la forme rectangle, ou alors en traçant une ligne le long d'un certain chemin puis en remplissant la forme. Nous allons vous montrer ci-dessous comment faire ces deux choses.</p>

<h3 id="Rectangles_simples">Rectangles simples</h3>

<p>Commençons avec quelques rectangles simples.</p>

<ol>
 <li>
  <p>Tout d'abord, faites une copie de votre template (ou copiez localement le fichier <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/1_canvas_template.html">1_canvas_template.html</a> si vous n'avez pas suivit les étapes précédentes).</p>
 </li>
 <li>
  <p>Ensuite, ajoutez les lignes suivantes au bas de votre JavaScript:</p>

  <pre class="brush: js">ctx.fillStyle = 'rgb(255, 0, 0)';
ctx.fillRect(50, 50, 100, 150);</pre>

  <p>Si vous sauvegardez votre code et rafraichissez la page, vous devriez voir qu'un rectangle rouge est apparu sur le canvas. Son coin supérieur gauche est à (50,50) pixels du coin supérieur gauche du canvas (comme définit par les deux premiers paramètres), il a une largeur de 100 pixels et une hauteur de 150 pixels (comme définit par les paramètres 3 et 4).</p>
 </li>
 <li>
  <p>Ajoutons un autre rectangle dans le mix — un vert cette fois. Ajoutez ce qui suit au bas de votre JavaScript:</p>

  <pre class="brush: js">ctx.fillStyle = 'rgb(0, 255, 0)';
ctx.fillRect(75, 75, 100, 100);</pre>

  <p>Sauvegardez et rafraichissez, et vous verrez un nouveau rectangle. Cela soulève un point important: les opérations graphiques comme dessiner des rectangles, lignes, et autres, sont executées dans l'ordre dans lequel elle apparaissent dans le code. Pensez-y comme peindre un mur, chaque couche de peinture s'ajoute par dessus les anciennes et peuvent même mettre cacher ce qu'il y a en dessous. Vous ne pouvez rien y faire, il faut donc réfléchir soigneusement à l'ordre dans lequel vous allez dessiner les éléments graphiques.</p>
 </li>
 <li>
  <p>Notez que vous pouvez dessiner des éléments graphiques semi-transparents en spécifiant une couleur semi-transparente, par exemple en utilisant <code>rgba()</code>. La valeur <code>a</code> définit ce qu'on appelle le "canal alpha", ou la quantité de transparence de la couleur. Plus la valeur de <code>a</code> est élevée, plus la couleur est opaque. Ajoutez ce qui suit à votre code:</p>

  <pre class="brush: js">ctx.fillStyle = 'rgba(255, 0, 255, 0.75)';
ctx.fillRect(25, 100, 175, 50);</pre>
 </li>
 <li>
  <p>Maintenant essayez de dessiner plus de rectangles par vous-même; amusez-vous!</p>
 </li>
</ol>

<h3 id="Traits_et_épaisseurs_de_ligne">Traits et épaisseurs de ligne</h3>

<p>Jusqu'à présent nous avons vu comment dessiner des rectangles pleins, mais on peut aussi ne dessiner que les contours (dit <strong>strokes</strong> - traits - en graphic design). Pour définir la couleur que vous voulez pour le contour, utilisez la propriété {{domxref("CanvasRenderingContext2D.strokeStyle", "strokeStyle")}}. Pour dessiner le contour du rectangle, on appelle {{domxref("CanvasRenderingContext2D.strokeRect", "strokeRect")}}.</p>

<ol>
 <li>
  <p>Ajoutez ce qui suit au bas de votre JavaScript:</p>

  <pre class="brush: js">ctx.strokeStyle = 'rgb(255, 255, 255)';
ctx.strokeRect(25, 25, 175, 200);</pre>
 </li>
 <li>
  <p>L'épaisseur de trait par défaut est de 1 pixel; vous pouvez ajuster la valeur de la propriété {{domxref("CanvasRenderingContext2D.lineWidth", "lineWidth")}} pour changer ça (prend un nombre spécifiant le nombre de pixels d'épaisseur de trait). Ajoutez la ligne suivante entre les deux lignes précédentes:</p>

  <pre class="brush: js">ctx.lineWidth = 5;</pre>

  <p>Vous devriez maintenant voir que votre contour blanc est devenu beaucoup plus épais!</p>
 </li>
</ol>

<p>C'est tout pour le moment. À ce stade votre exemple devrait ressembler à ça:</p>

<p>{{EmbedGHLiveSample("learning-area/javascript/apis/drawing-graphics/getting-started/2_canvas_rectangles.html", '100%', 250)}}</p>

<div class="note">
<p><strong>Note :</strong> Le code terminé est disponible sur GitHub, <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/2_canvas_rectangles.html">2_canvas_rectangles.html</a>.</p>
</div>

<h3 id="Dessiner_des_chemins">Dessiner des chemins</h3>

<p>Si vous voulez dessiner quelque chose de plus complexe qu'un rectangle, vous allez certainement devoir utiliser un <em>path</em> (chemin). En gros, cela implique de spécifier exactement où déplacer un stylo sur le canvas pour tracer la forme que vous voulez. L'API Canvas inclut des fonctions pour dessiner des lignes droites, des cercles, des courbes Bézier, et plus encore.</p>

<p>Commençons la section en faisant une nouvelle copie de notre template (<a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/1_canvas_template.html">1_canvas_template.html</a>), dans lequel nous allons dessiner le nouvel exemple.</p>

<p>Nous allons utiliser quelques méthodes et propriétés communes dans les sections suivantes:</p>

<ul>
 <li>{{domxref("CanvasRenderingContext2D.beginPath", "beginPath()")}} — commence à dessiner un path au point où le stylo se situe sur le canvas. Sur un nouveau canvas, le stylo commence au point (0, 0).</li>
 <li>{{domxref("CanvasRenderingContext2D.moveTo", "moveTo()")}} — déplace le stylo à un point différent sur le canvas, sans tracer de ligne; le stylo "saute" simplement à une nouvelle position.</li>
 <li>{{domxref("CanvasRenderingContext2D.fill", "fill()")}} — dessine une forme en remplissant le path définit jusqu'à présent.</li>
 <li>{{domxref("CanvasRenderingContext2D.stroke", "stroke()")}} — dessine un trait en suivant le path définit jusqu'à présent.</li>
 <li>Vous pouvez utiliser les fonctionnalités telles que <code>lineWidth</code> et <code>fillStyle</code>/<code>strokeStyle</code> avec les paths aussi bien qu'avec les rectangles.</li>
</ul>

<p>Typiquement, une manière de dessiner un trait simple ressemblerait à ça:</p>

<pre class="brush: js">ctx.fillStyle = 'rgb(255, 0, 0)';
ctx.beginPath();
ctx.moveTo(50, 50);
// tracer le trait
ctx.fill();</pre>

<h4 id="Dessiner_des_lignes">Dessiner des lignes</h4>

<p>Dessinons un triangle équilatéral sur le canvas.</p>

<ol>
 <li>
  <p>Tout d'abord, ajoutez la fonction d'aide suivante au bas de votre code. Elle convertit des valeurs en degrés en radians, ce qui est utile car chaque fois que vous devez fournir une valeur d'angle en JavaScript, ce sera presque toujours en radians, tandis que les humains pensent généralement en degrés.</p>

  <pre class="brush: js">function degToRad(degrees) {
  return degrees * Math.PI / 180;
};</pre>
 </li>
 <li>
  <p>Ensuite, commencez votre path en ajoutant ce qui suit au bas de votre JavaScript. Ici, nous définissons une couleur pour notre triangle et déplaçons le stylo au point (50, 50) sans rien tracer. C'est à partir de là que nous allons dessiner notre triangle.</p>

  <pre class="brush: js">ctx.fillStyle = 'rgb(255, 0, 0)';
ctx.beginPath();
ctx.moveTo(50, 50);</pre>
 </li>
 <li>
  <p>Maintenant ajoutez le bloc de code suivant:</p>

  <pre class="brush: js">ctx.lineTo(150, 50);
var triHeight = 50 * Math.tan(degToRad(60));
ctx.lineTo(100, 50+triHeight);
ctx.lineTo(50, 50);
ctx.fill();</pre>

  <p>Parcourons ceci dans l'ordre:</p>

  <ol>
   <li>
    <p>D'abord nous ajoutons une ligne vers (150, 50) — notre path va maintenant 100 pixels vers la droite le long de l'axe horizontal (x).</p>
   </li>
   <li>
    <p>Puis, nous calculons la hauteur de notre triangle équilatéral, en utilisant un peu de trigonométrie simple. Nous dessinons un triangle pointant vers le bas.</p>

    <p>Les angles d'un triangle équilatéral sont tous de 60 degrés. Pour calculer la hauteur, nous pouvons séparer le triangle en deux triangles rectangles par le milieu, qui auront alors des angles de 90, 60 et 30 degrés.</p>

    <p>Pour ce qui est des côtés:</p>

    <ul>
     <li>Le côté le plus long est appelé l'<strong>hypoténuse</strong></li>
     <li>Le côté relié à l'angle de 60 degrés (et qui n'est pas l'hypothénuse) est dit <strong>adjacent</strong> à cet angle — sa longueur est de 50 pixels puisque c'est la moitié de la ligne que nous avons dessiné.</li>
     <li>Le côté opposé à l'angle de 60 degrés est dit <strong>opposé</strong> à cet angle — c'est la hauteur que nous voulons calculer.</li>
    </ul>

    <p> </p>

    <p><img alt="" src="trigonometry.png"></p>

    <p>Une des formule trigonométrique de base stipule que la longueur du côté adjacent mutiplié par la tangente de l'angle est égale à l'opposé, soit <code>50 * Math.tan(degToRad(60))</code>. Nous utilisons notre fonction <code>degToRad()</code> pour convertir 60 degrés en radians, puisque {{jsxref("Math.tan()")}} attend une valeur en radians.</p>
   </li>
   <li>
    <p>Avec la hauteur calculée, nous ajoutons une nouvelle ligne vers <code>(100, 50+triHeight)</code>. La coordonnée X est simple, elle est à mi-chemin de la ligne que nous avons tracé. La valeur de Y d'autre part doit être de 50 plus la hauteur du triangle, puisque le haut du triangle est à 50 pixels du haut du canvas.</p>
   </li>
   <li>
    <p>L'instruction qui suit ajoute une ligne vers le point de départ du triangle.</p>
   </li>
   <li>
    <p>Pour finir, nous appelons <code>ctx.fill()</code> pour finir le path et remplir la forme.</p>
   </li>
  </ol>
 </li>
</ol>

<h4 id="Dessiner_des_cercles">Dessiner des cercles</h4>

<p>Maintenant, voyons comment dessiner un cercle sur le canvas. Pour ce faire, on utilise la méthode {{domxref("CanvasRenderingContext2D.arc", "arc()")}}, qui dessine tout ou une portion de cercle à un point spécifié.</p>

<ol>
 <li>
  <p>Ajoutons un arc à notre canvas en ajoutant le code qui suit:</p>

  <pre class="brush: js">ctx.fillStyle = 'rgb(0, 0, 255)';
ctx.beginPath();
ctx.arc(150, 106, 50, degToRad(0), degToRad(360), false);
ctx.fill();</pre>

  <p><code>arc()</code> prend six paramètres.</p>

  <ul>
   <li>Les deux premiers spécifient la position du centre du cercle (X et Y respectivement).</li>
   <li>Le troisième est le rayon du cercle</li>
   <li>Le quatrième et le cinquième sont les angles de début et de fin pour dessiner l'arc (donc spécifier 0 et 360 nous donne un cercle fermé)</li>
   <li>Et le sixième paramètre définit si le cercle doit être dessiné dans le sens des aiguilles d'une montre ou dans le sens inverse (<code>false</code> pour le sens horaire).</li>
  </ul>

  <div class="note">
  <p><strong>Note :</strong> 0 degrés est horizontalement vers la droite.</p>
  </div>
 </li>
 <li>
  <p>Ajoutons un autre arc:</p>

  <pre class="brush: js">ctx.fillStyle = 'yellow';
ctx.beginPath();
ctx.arc(200, 106, 50, degToRad(-45), degToRad(45), true);
ctx.lineTo(200, 106);
ctx.fill();</pre>

  <p>Le motif ici est très similaire, a deux différences près:</p>

  <ul>
   <li>Nous avons mis le dernier paramètre de <code>arc()</code> à <code>true</code>, ce qui signifie que l'arc est tracé dans le sens inverse des aiguilles d'une montre.  Donc si notre arc commence à -45 degrés et fini à 45 degrés, nous dessinons un arc de 270 degrés. Si vous changez <code>true</code> à <code>false</code> et ré-exécutez le code, seule une portion de 90 degrés sera dessinée.</li>
   <li>Avant d'appeler <code>fill()</code>, nous ajoutons une ligne vers le centre du cercle. Nous obtenons une découpe de style Pac-Man plutôt sympa. Si vous supprimiez cette ligne (essayez!) et ré-exécutiez le code, vous auriez juste un cercle dont le bout a été coupé — entre le début et la fin de l'arc. Cela illuste un autre point important du canvas: si vous essayez de remplir une forme incomplète (qui n'est pas fermée), le navigateur ajoute une ligne droite entre le début et la fin du path et le remplit.</li>
  </ul>
 </li>
</ol>

<p>C'est tout pour le moment; votre exemple final devrait ressembler à ceci:</p>

<p>{{EmbedGHLiveSample("learning-area/javascript/apis/drawing-graphics/getting-started/3_canvas_paths.html", '100%', 200)}}</p>

<div class="note">
<p><strong>Note :</strong> Le code finit est disponible sur GitHub, <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/3_canvas_paths.html">3_canvas_paths.html</a>.</p>
</div>

<div class="note">
<p><strong>Note :</strong> Pour en savoir plus sur les fonctions de dessin avancées, telles que les courbes Bézier, consultez notre tutoriel <a href="/fr/docs/Tutoriel_canvas/Formes_géométriques">Dessiner des formes avec le canevas</a>.</p>
</div>

<h3 id="Texte">Texte</h3>

<p>Canvas dispose également de fonctionnalités pour écrire du texte. Nous allons les explorer brièvement. Commencez par créer une nouvelle copie du template (<a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/1_canvas_template.html">1_canvas_template.html</a>), dans lequel nous allons dessiner le nouvel exemple.</p>

<p>Le texte peut être avec deux méthodes:</p>

<ul>
 <li>{{domxref("CanvasRenderingContext2D.fillText", "fillText()")}} — dessine un texte rempli.</li>
 <li>{{domxref("CanvasRenderingContext2D.strokeText", "strokeText()")}} — dessine un contour de texte.</li>
</ul>

<p>Ces deux méthodes prennent trois paramètres: la chaîne de caractères à écrire et les coordonnées X et Y du coin supérieur gauche de la zone de texte (<strong>text box</strong>) — littéralement, la zone entourant le texte que vous écrivez.</p>

<p>Il existe également un certain nombre de proprétés pour contrôler le rendu du texte, comme {{domxref("CanvasRenderingContext2D.font", "font")}}, qui permer de spécifier la police d'écriture, la taille, etc — elle accepte la même syntaxe que la propriété CSS {{cssxref("font")}}.</p>

<p>Essayez d'ajouter le bloc suivant au bas de votre javaScript:</p>

<pre class="brush: js">ctx.strokeStyle = 'white';
ctx.lineWidth = 1;
ctx.font = '36px arial';
ctx.strokeText('Canvas text', 50, 50);

ctx.fillStyle = 'red';
ctx.font = '48px georgia';
ctx.fillText('Canvas text', 50, 150);</pre>

<p>Ici nous dessinons deux lignes de texte, une avec le contour et l'autre remplie. L'exemple final devrait ressembler à ça:</p>

<p>{{EmbedGHLiveSample("learning-area/javascript/apis/drawing-graphics/getting-started/4_canvas_text.html", '100%', 180)}}</p>

<div class="note">
<p><strong>Note :</strong> Le code final est disponible sur GitHub, <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/4_canvas_text.html">4_canvas_text.html</a>.</p>
</div>

<p>Jouez avec et voyez ce que vous pouvez faire! Vous pouvez trouver plus d'information sur les options disponibles pour ajouter du texte sur un canvas dans <a href="/fr/docs/Dessin_de_texte_avec_canvas">Dessin de texte avec canvas</a>.</p>

<h3 id="Dessiner_des_images_sur_le_canvas">Dessiner des images sur le canvas</h3>

<p>Il est possible d'afficher des images externes sur le canvas. Ce peut être des images simples, des images à l'intérieur d'une vidéo, ou le contenu d'autres canvas. Pour le moment, nous allons juste nous occuper d'ajouter des images simples sur le canvas.</p>

<ol>
 <li>
  <p>Comme précédemment, créez une nouvelle copie du template (<a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/1_canvas_template.html">1_canvas_template.html</a>), où nous dessinerons l'exemple. Vous allez également devoir sauvegarder une copie de notre image d'exemple — <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/firefox.png">firefox.png</a> — dans le même répertoire.</p>

  <p>Les images sont dessinés sur le canvas en utilisant la méthode {{domxref("CanvasRenderingContext2D.drawImage", "drawImage()")}}. Dans sa version la plus simple, elle prend trois paramètres — une référence de l'image que vous voulez afficher et les coordonnées X et Y du coin supérieur gauche de l'image sur le canvas.</p>
 </li>
 <li>
  <p>Commençons par obtenir une ressource de l'image à inclure dans notre canvas. Ajoutez les lignes suivantes au bas de votre JavaScript:</p>

  <pre class="brush: js">var image = new Image();
image.src = 'firefox.png';</pre>

  <p>Ici, nous créons un nouvel objet {{domxref("HTMLImageElement")}} en utilisant le constructeur {{domxref("HTMLImageElement.Image()", "Image()")}}. (L'objet retourné est le même type que celui retourné lorsque vous récupérez une référence vers un élément {{htmlelement("img")}} existant). Nous définissons son attribut  {{htmlattrxref("src", "img")}} à notre image du logo Firefox. À ce stade, le navigateur commence à charger l'image.</p>
 </li>
 <li>
  <p>Nous pourrions essayer maintenant d'inclure l'image en utilisant <code>drawImage()</code>, mais nous devons nous assurer que le fichier image ait été chargé en premier, faute de quoi le code échouera. Nous pouvons y parvenir en utilisant le gestionnaire d'événement <code>onload</code>, qui ne sera appelé que lorsque l'image aura fini de charger. Ajoutez le bloc suivant à la suite du précédent:</p>

  <pre class="brush: js">image.onload = function() {
  ctx.drawImage(image, 50, 50);
}</pre>

  <p>Si vous chargez votre exemple dans le navigateur maintenant, vous devriez voir l'image inclue dans le canvas.</p>
 </li>
 <li>
  <p>Mais il y en a plus! Et si nous ne voulions afficher qu'une partie de l'image, ou la redimensionner? Nous pouvons faire ces deux choses avec une version plus complexe de <code>drawImage()</code>. Mettez à jour votre ligne <code>ctx.drawImage()</code> comme suit:</p>

  <pre class="brush: js">ctx.drawImage(image, 20, 20, 185, 175, 50, 50, 185, 175);</pre>

  <ul>
   <li>Le premier paramètre est la référence de l'image, comme précédemment.</li>
   <li>Les paramètres 2 et 3 définissent les coordonnées à partir d'où découper l'image, relativement au coin supérieur gauche de l'image d'origine. Tout ce qui est à gauche de X (paramètre 2) ou au-dessus de Y (paramètre 3) ne sera pas dessiné.</li>
   <li>Les paramètres 4 et 5 définissent la largeur et hauteur de la zone que nous voulons découper, à partir du coin supérieur gauche de l'image découpée.</li>
   <li>Les paramètres 6 et 7 définissent les coordonnées où vous souhaitez placer l'image sur le canvas, relativement au coin supérieur gauche du canvas.</li>
   <li>Les paramètres 8 et 9 définissent la largeur et la hauteur affichée de l'image découpée. En l'occurence, nous avons spécifié les mêmes dimensions que la découpe, mais vous pouvez la redimensionner (et la déformer) en spécifiant des valeurs différentes.</li>
  </ul>
 </li>
</ol>

<p>L'exemple final devrait ressembler à ça:</p>

<p>{{EmbedGHLiveSample("learning-area/javascript/apis/drawing-graphics/getting-started/5_canvas_images.html", '100%', 260)}}</p>

<div class="note">
<p><strong>Note :</strong> Le code final est disponible sur GitHub, <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/5_canvas_images.html">5_canvas_images.html</a>.</p>
</div>

<h2 id="Boucles_et_animations">Boucles et animations</h2>

<p>Jusqu'ici, nous avons couvert quelques utilisations très basiques du canvas 2D, mais vous ne ressentirez la pleine puissance du canvas que si vous le mettez à jour ou l'animez d'une manière ou d'une autre. Après tout, le canvas fournit des images scriptables! Si vous n'avez pas l'intention de changer quelque chose, alors autant utiiliser des images statiques et vous épargner du travail.</p>

<h3 id="Créer_une_boucle">Créer une boucle</h3>

<p>Jouer avec des boucles est plutôt amusant — vous pouvez exécuter des commandes de canvas à l'intérieur d'une boucle <code><a href="/fr/docs/Web/JavaScript/Reference/Instructions/for">for</a></code> (ou tout autre type de boucle) comme n'importe quel autre code JavaScript.</p>

<p>Construisons un exemple simple.</p>

<ol>
 <li>
  <p>Créez une nouvelle copie du template (<a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/1_canvas_template.html">1_canvas_template.html</a>) et ouvrez-le dans votre éditeur de texte.</p>
 </li>
 <li>
  <p>Ajoutez la ligne qui suit au bas de votre JavaScript. Elle contient une nouvelle méthode, {{domxref("CanvasRenderingContext2D.translate", "translate()")}}, qui déplace le point d'origine du canvas:</p>

  <pre class="brush: js">ctx.translate(width/2, height/2);</pre>

  <p>Cela a pour effet de déplacer l'origine des coordonnées (0, 0) au centre du canvas, plutôt que d'être dans le coin supérieur gauche. C'est très utile dans de nombreuses situations, comme celle-ci, où nous voulons que notre dessin soit dessiné par rapport au centre du canvas.</p>
 </li>
 <li>
  <p>Maintenant ajoutez le code suivant au bas du Javacript:</p>

  <pre class="brush: js">function degToRad(degrees) {
  return degrees * Math.PI / 180;
};

function rand(min, max) {
  return Math.floor(Math.random() * (max-min+1)) + (min);
}

var length = 250;
var moveOffset = 20;

for(var i = 0; i &lt; length; i++) {

}</pre>

  <p>Ici, nous implémentons</p>

  <ul>
   <li>la même fonction <code>degToRad()</code> que nous avons vu dans l'exemple du triangle auparavant,</li>
   <li>une fonction <code>rand()</code>, qui retoune un nombre aléatoire entre une limite inférieure et une limite supérieure,</li>
   <li>les variables <code>length</code> et <code>moveOffset</code> (que nous verrons plus loin),</li>
   <li>et une boucle <code>for</code> vide.</li>
  </ul>
 </li>
 <li>
  <p>L'idée est que nous allons dessiner quelque chose sur le canvas à l'intérieur de la boucle <code>for</code>, et itérer dessus pour créer quelque chose d'intéressant. Ajoutez le code suivant à l'intérieur de la boucle <code>for</code>:</p>

  <pre class="brush: js">ctx.fillStyle = 'rgba(' + (255-length) + ', 0, ' + (255-length) + ', 0.9)';
ctx.beginPath();
ctx.moveTo(moveOffset, moveOffset);
ctx.lineTo(moveOffset+length, moveOffset);
var triHeight = length/2 * Math.tan(degToRad(60));
ctx.lineTo(moveOffset+(length/2), moveOffset+triHeight);
ctx.lineTo(moveOffset, moveOffset);
ctx.fill();

length--;
moveOffset += 0.7;
ctx.rotate(degToRad(5));</pre>

  <p>Ainsi à chaque itération, on:</p>

  <ol>
   <li>Définit <code>fillStyle</code> comme étant une nuance de violet légèrement transparente, et qui change à chaque fois en fonction de la valeur de <code>length</code>. Comme vous le verrez plus tard, sa valeur diminue à chaque itération, ce qui a pour effet de rendre la couleur toujours plus claire.</li>
   <li>Ouvre un path.</li>
   <li>Déplace le stylo aux coordonnées de <code>(moveOffset, moveOffset)</code>; Cette variable définit jusqu'où nous voulons nous déplacer à chaque fois que nous dessinons.</li>
   <li>Dessine une ligne aux coordonées de <code>(moveOffset+length, moveOffset)</code>. Cela dessine une ligne de longueur <code>length</code> parallèle à l'axe X.</li>
   <li>Calcule la hauteur du triangle, comme vu auparavant.</li>
   <li>Dessine une ligne vers le coin du bas du triangle.</li>
   <li>Dessine une ligne vers le début du triangle.</li>
   <li>Appelle <code>fill()</code> pour remplir le triangle.</li>
   <li>Met à jour les variables qui indiquent comment dessiner le triangle, afin qu'elles soient prêtes pour la prochaine itération:
    <ul>
     <li>Diminue la valeur de <code>length</code> de 1, de sorte que les triangles deviennent de plus en plus petits;</li>
     <li>Augmente un peu <code>moveOffset</code> pour que chaque triangle successif soit légèrement plus éloigné;</li>
     <li>et utilise une nouvelle fonction, {{domxref("CanvasRenderingContext2D.rotate", "rotate()")}}, qui permet de faire pivoter entièrement le canvas! Nous le faisons pivoter de 5 degrés avant de dessiner le triangle suivant.</li>
    </ul>
   </li>
  </ol>
 </li>
</ol>

<p>C'est tout! L'exemple final devrait ressemble à ça:</p>

<p>{{EmbedGHLiveSample("learning-area/javascript/apis/drawing-graphics/loops_animation/6_canvas_for_loop.html", '100%', 550)}}</p>

<p>À ce stade, nous vous encourageons à jouer avec l'exemple et de vous l'approprier! Par exemple:</p>

<ul>
 <li>Dessinez des rectangles ou des arcs au lieu des triangles, ou même des images externes.</li>
 <li>Jouez avec les valeurs de <code>length</code> et <code>moveOffset</code>.</li>
 <li>Utilisez des nombres aléatoires — grâce à la fonction <code>rand()</code> que nous avons inclue mais que nous n'avons pas utilisée.</li>
</ul>

<div class="note">
<p><strong>Note :</strong> Le code terminé est disponible sur GitHub, <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/loops_animation/6_canvas_for_loop.html">6_canvas_for_loop.html</a>.</p>
</div>

<h3 id="Animations">Animations</h3>

<p>L'exemple de boucle que nous avons construit ci-dessus était amusant, mais en vrai vous avez besoin d'une boucle qui continue constamment d'itérer pour toute application sérieuse de canvas (telles que les jeux et les visualisations en temps réel). Si vous pensez à votre canvas comme étant en quelque sorte un film, vous allez vouloir que l'affichage se mette à jour à chaque image pour afficher la mise à jour avec un taux de rafraichissement idéal de 60 images par seconde, afin que le mouvement soit lisse et agréable pour l'oeil humain.</p>

<p>Il y a quelques fonctions JavaScript qui vous permettrons d'exécuter des fonctions de manière répétée, plusieurs fois par seconde, la meilleure étant ici {{domxref("window.requestAnimationFrame()")}}. Elle prend un paramètre — la fonction que vous voulez exécuter pour chaque image. Dès que le navigateur est prêt à mettre à jour l'écran, votre fonction sera appelée. Si cette fonction dessine la nouvelle mise à jour, puis appelle de nouveau <code>requestAnimationFrame()</code> juste avant la fin de la fonction, la boucle d'animation continuera de s'exécuter de manière fluide. La boucle s'arrête lorsque vous vous arrêtez d'appeler <code>requestAnimationFrame()</code> ou si vous appelez {{domxref("window.cancelAnimationFrame()")}} après avoir appelé <code>requestAnimationFrame()</code> mais avant que votre fonction n'ait été exécutée.</p>

<div class="note">
<p><strong>Note:</strong> C'est une bonne pratique d'appeler <code>cancelAnimationFrame()</code> à partir de votre code principal lorsque vous avez terminé d'utiliser l'animation, pour vous assurer qu'aucune mise à jour n'attend d'être exécutée.</p>
</div>

<p>Le navigateur s'occupe des détails complexes tels qu'exécuter l'animation à une vitesse constante, et ne pas gaspiller de ressources en animant des choses qui ne sont pas visibles.</p>

<p>Pour voir comment cela fonctionne, regardons rapidement notre exemple des balles qui rebondissent (<a href="https://mdn.github.io/learning-area/javascript/oojs/bouncing-balls/index-finished.html">le voir en direct</a>, et voir <a href="https://github.com/mdn/learning-area/tree/master/javascript/oojs/bouncing-balls">le code source</a>). Le code de la boucle qui garde le tout en mouvement ressemble à ceci:</p>

<pre class="brush: js">function loop() {
  ctx.fillStyle = 'rgba(0, 0, 0, 0.25)';
  ctx.fillRect(0, 0, width, height);

  while(balls.length &lt; 25) {
    var ball = new Ball();
    balls.push(ball);
  }

  for(i = 0; i &lt; balls.length; i++) {
    balls[i].draw();
    balls[i].update();
    balls[i].collisionDetect();
  }

  requestAnimationFrame(loop);
}

loop();</pre>

<p>Nous lançons la fonction <code>loop()</code> une fois pour commencer le cycle et dessiner la première image de l'animation. La fonction <code>loop()</code> s'occupe ensuite d'appeler <code>requestAnimationFrame(loop)</code> pour afficher la prochaine image de l'animation, et ce continuellement.</p>

<p>Notez que sur chaque image, nous effaçons complètement le canvas et redessinons tout. Nous créons de nouvelles balles pour chaque image — au maximum 25 — puis, pour chaque balle, la dessinons, mettons à jour sa position, et vérifions si elle est en collision avec une autre balle. Une fois que vous avez dessiné quelque chose sur un canvas, il n'y a aucun moyen pour manipuler cet élément graphique individuellement comme vous pouvez le faire avec les élément DOM. Vous ne pouvez pas déplacer les balles sur le canvas parce qu'une fois dessinée, une balle n'est plus une balle mais juste des pixels sur un canvas. Au lieu de ça, vous devez effacer et redessiner, soit en effaçant et redessinant absolutement tout le canvas, soit en ayant du code qui sait exactement quelles parties doivent être effacées, et qui efface et redessine uniquement la zone minimale nécessaire.</p>

<p>Optimiser l'animation graphique est une spécialité entière de programmation, avec beaucoup de techniques ingénieuses disponibles. Mais celles-ci sont au-delà de ce dont nous avons besoin pour notre exemple!</p>

<p>En général, le processus pour animer un canvas implique les étapes suivantes:</p>

<ol>
 <li>Effacer le contenu du cavas (par exemple avec {{domxref("CanvasRenderingContext2D.fillRect", "fillRect()")}} ou {{domxref("CanvasRenderingContext2D.clearRect", "clearRect()")}}).</li>
 <li>Sauvegarder l'état (si nécessaire) en utilisant {{domxref("CanvasRenderingContext2D.save", "save()")}} — c'est nécessaire lorsque vous voulez enregistrer les paramètres que vous mis à jour sur le canvas avant de continuer, ce qui est utile pour des applications plus avancées.</li>
 <li>Dessiner les éléments graphiques que vous animez.</li>
 <li>Restaurer les paramètres sauvegardés à l'étape 2 en utilisant {{domxref("CanvasRenderingContext2D.restore", "restore()")}}</li>
 <li>Appeler <code>requestAnimationFrame()</code> pour planifier le dessin de l'image suivante de l'animation.</li>
</ol>

<div class="note">
<p><strong>Note :</strong> Nous ne couvrirons pas <code>save()</code> et <code>restore()</code> ici, mais elles sont bien expliquées dans notre tutoriel <a href="/fr/docs/Tutoriel_canvas/Transformations">Transformations</a> (et ceux qui le suivent).</p>
</div>

<h3 id="Une_animation_simple_de_personnage">Une animation simple de personnage</h3>

<p>Créons maintenant notre propre animation simple — nous allons faire parcourir l'écran à un personnage d'un certain jeu vidéo rétro plutôt génial.</p>

<ol>
 <li>
  <p>Faites une nouvelle copie du template (<a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/getting-started/1_canvas_template.html">1_canvas_template.html</a>) et ouvrez-le dans votre éditeur de texte. Sauvegardez une copie de <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/loops_animation/walk-right.png">walk-right.png</a> dans le même répertoire.</p>
 </li>
 <li>
  <p>Au bas du JavaScript, ajoutez la ligne suivante pour placer une fois de plus l'origine des coordonnées au milieu du canvas:</p>

  <pre class="brush: js">ctx.translate(width/2, height/2);</pre>
 </li>
 <li>
  <p>Nous allons maintenant créer un objet {{domxref("HTMLImageElement")}}, définir son attribut {{htmlattrxref("src", "img")}} à l'image que nous voulons charger, et ajouter le gestionnaire d'événement <code>onload</code> pour appeler la fonction <code>draw()</code> quand l'image sera chargée:</p>

  <pre class="brush: js">var image = new Image();
image.src = 'walk-right.png';
image.onload = draw;</pre>
 </li>
 <li>
  <p>Ajoutons quelques variables pour garder une trace de la position du sprite à dessiner à l'écran, et le numéro du sprite que nous voulons afficher.</p>

  <pre class="brush: js">var sprite = 0;
var posX = 0;</pre>

  <p>L'image de sprites (que nous avons respectueusement emprunté à Mike Thomas dans son article <a href="http://atomicrobotdesign.com/blog/htmlcss/create-a-sprite-sheet-walk-cycle-using-using-css-animation/" rel="bookmark" title="Permanent Link to Create a sprite sheet walk cycle using using CSS animation">Create a sprite sheet walk cycle using using CSS animation</a> — créer un cycle de marche avec une feuille de sprites en utilisant les animations CSS) ressemble à ça:</p>

  <p><img alt="" src="walk-right.png"></p>

  <p>Elle contient six sprites qui constituent une séquence de marche — chacun a 102 pixels de large et 148 pixels de hauteur. Pour afficher chaque sprite proprement, nous allons devoir utiliser <code>drawImage()</code> pour découper un seul sprite de l'image et n'afficher que cette partie, comme nous l'avons fait précédemment avec le logo Firefox. La coordonnée X de la découpe devra être un multiple de 102 et la coordonnée Y sera toujours 0. La taille de la découpe sera toujours de 102 pixels par 148.</p>
 </li>
 <li>
  <p>Insérons maintenant une fonction <code>draw()</code> vide au bas du code, prête à être remplie de code:</p>

  <pre class="brush: js">function draw() {

};</pre>
 </li>
 <li>
  <p>Le reste du code dans cette section va dans <code>draw()</code>. Tout d'abord, ajoutez la ligne suivante, qui efface le canvas pour préparer le dessin de chaque image. Notez que nous devons spécifier le coin supérieur gauche du rectangle comme étant <code>-(width/2), -(height/2)</code> puisque nous avons définit l'origine du canvas à <code>width/2, height/2</code> plus tôt.</p>

  <pre class="brush: js">ctx.fillRect(-(width/2), -(height/2), width, height);</pre>
 </li>
 <li>
  <p>Ensuite, nous allons dessinons notre image en utilisant <code>drawImage()</code> — la version à 9 paramètres. Ajoutez ce qui suit:</p>

  <pre class="brush: js">ctx.drawImage(image, (sprite*102), 0, 102, 148, 0+posX, -74, 102, 148);</pre>

  <p>Comme vous pouvez le voir:</p>

  <ul>
   <li>Nous spécifions <code>image</code> comme étant l'image à inclure.</li>
   <li>Les paramètres 2 et 3 spécifient le coin supérieur gauche de la portion de l'image à découper: la valeur X vaut <code>sprite</code> multiplié par 102 (où <code>sprite</code> est le numéro du sprite, entre 0 et 5) et la valeur Y vaut toujours 0.</li>
   <li>Les paramètres 4 et 5 spécifient la taille de la découpe — 102 pixels par 148.</li>
   <li>Les paramètres 6 et 7 spécifient le coin supérieur gauche de la découpe sur le canvas — la position de X est <code>0+posX</code>, ce qui signifie que nous pouvons modifier la position du dessin en modifiant la valeur de <code>posX</code>.</li>
   <li>Les paramètres 8 et 9 spécifient la taille de l'image sur le canvas. Nous voulons garder sa taille d'origine, on définit donc 102 pour largeur et 148 pour hauteur.</li>
  </ul>
 </li>
 <li>
  <p>Maintenant, nous allons changer la valeur de <code>sprite</code> après chaque dessin — après certains d'entre eux du moins. Ajoutez le bloc de code suivant au bas de la fonction <code>draw()</code>:</p>

  <pre class="brush: js">  if (posX % 13 === 0) {
    if (sprite === 5) {
      sprite = 0;
    } else {
      sprite++;
    }
  }</pre>

  <p>Nous enveloppons le bloc entier de <code>if (posX % 13 === 0) { ... }</code>. On utilise l'opérateur modulo (<code>%</code>) (aussi connu sous le nom d'<a href="/fr/docs/Web/JavaScript/Reference/Opérateurs/Opérateurs_arithmétiques#Reste_()">opérateur reste</a>) pour vérifier si la valeur de <code>posX</code> peut être exactement divisée par 13, sans reste. Si c'est le cas, on passe au sprite suivant en incrémentant <code>sprite</code> (en retournant à 0 après le sprite #5). Cela implique que nous ne mettons à jour le sprite que toutes les 13èmes images, ou à peu près 5 images par seconde (<code>requestAnimationFrame()</code> appelle jusqu'à 60 images par secondes si possible). Nous ralentissons délibéremment le cadence des images parce que nous n'avons que six sprites avec lesquels travailler, et si on en affiche un à chaque 60ième de seconde, notre personnage va bouger beaucoup trop vite!</p>

  <p>À l'intérieur du bloc, on utilise une instruction <code><a href="/fr/docs/Web/JavaScript/Reference/Instructions/if...else">if ... else</a></code> pour vérifier si la valeur de <code>sprite</code> vaut 5 (le dernier sprite, puisque les numéro de sprite vont de 0 à 5). Si nous sommes en train d'afficher le dernier sprite, alors on réinitialilse <code>sprite</code> à 0; sinon on l'incrémente de 1.</p>
 </li>
 <li>
  <p>Ensuite, nous devons déterminer comment modifier la valeur de <code>posX</code> sur chaque image — ajoutez le bloc de code à la suite:</p>

  <pre class="brush: js">  if(posX &gt; width/2) {
    newStartPos = -((width/2) + 102);
    posX = Math.ceil(newStartPos / 13) * 13;
    console.log(posX);
  } else {
    posX += 2;
  }</pre>

  <p>Nous utilisons une autre instruction <code>if ... else</code> pour voir si la valeur de <code>posX</code> est plus grande que <code>width/2</code>, ce qui signifie que notre personnage est sortit du bord droit de l'écran. Si c'est le cas, on calcule la position qui met le personnage à gauche du bord gauche de l'écran, et on définit <code>posX</code> au multiple de 13 le plus proche de ce nombre. Il faut obligatoirement un multiple de 13 pour que le bloc de code précédent puisse toujours fonctionner!</p>

  <p>Si notre personnage n'a pas atteint le bord de l'écran, on incrémente <code>posX</code> de 2. Cela le fera bouger un peu vers la droite la prochaine fois qu'on le dessinera.</p>
 </li>
 <li>
  <p>Finalement, nous devons boucler sur l'animation en appelannt {{domxref("window.requestAnimationFrame", "requestAnimationFrame()")}} en bas de la fonction <code>draw()</code>:</p>

  <pre class="brush: js">window.requestAnimationFrame(draw);</pre>
 </li>
</ol>

<p>Et voilà! L'exemple final devrait ressembler à ça:</p>

<p>{{EmbedGHLiveSample("learning-area/javascript/apis/drawing-graphics/loops_animation/7_canvas_walking_animation.html", '100%', 260)}}</p>

<div class="note">
<p><strong>Note :</strong> Le code final est disponible sur GitHub, <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/loops_animation/7_canvas_walking_animation.html">7_canvas_walking_animation.html</a>.</p>
</div>

<h3 id="Une_application_simple_de_dessin">Une application simple de dessin</h3>

<p>Comme exemple final d'animation, nous aimerions vous montrer une application très simple de dessin, pour illustrer comment la boucle d'animation peut être combinée avec les entrées de l'utilisateur (comme le mouvement de la souris en l'occurence). Nous n'allons pas expliquer la procédure pas à pas pour construire cette application, nous allons juste explorer les parties les plus intéressantes du code.</p>

<p>L'exemple peut être trouvé sur GitHub, <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/loops_animation/8_canvas_drawing_app.html">8_canvas_drawing_app.html</a>, et vous pouvez jouer avec en direct ci-dessous:</p>

<p>{{EmbedGHLiveSample("learning-area/javascript/apis/drawing-graphics/loops_animation/8_canvas_drawing_app.html", '100%', 600)}}</p>

<p>Regardons les parties les plus intéressantes. Tout d'abord, nous gardons une trace des coordonnées X et Y de la souris et si elle est pressée ou non grâce à trois variables: <code>curX</code>, <code>curY</code>, et <code>pressed</code>. Quand la souris bouge, nous déclenchons une fonction via le gestionnaire d'événement <code>onmousemove</code>, lequel capture les valeurs X et Y actuelles. Nous utilisons également les gestionnaires d'événement <code>onmousedown</code> et <code>onmouseup</code> pour changer la valeur de <code>pressed</code> à <code>true</code> quand le bouton de la souris est pressé, et de nouveau à <code>false</code> quand il est relaché.</p>

<pre class="brush: js">var curX;
var curY;
var pressed = false;

document.onmousemove = function(e) {
  curX = (window.Event) ? e.pageX : e.clientX + (document.documentElement.scrollLeft ? document.documentElement.scrollLeft : document.body.scrollLeft);
  curY = (window.Event) ? e.pageY : e.clientY + (document.documentElement.scrollTop ? document.documentElement.scrollTop : document.body.scrollTop);
}

canvas.onmousedown = function() {
  pressed = true;
};

canvas.onmouseup = function() {
  pressed = false;
}</pre>

<p>Quand le bouton "Clear canvas" (effacer le canvas) est cliqué, nous exécutons une simple fonction qui efface entièrement le canvas grâce à un rectangle noir, de la même manière que nous avons vu précédemment:</p>

<pre class="brush: js">clearBtn.onclick = function() {
  ctx.fillStyle = 'rgb(0, 0, 0)';
  ctx.fillRect(0, 0, width, height);
}</pre>

<p>La boucle du dessin est relativement simple cette fois-ci — si <code>pressed</code> est à <code>true</code>, nous dessinons un cercle rempli avec la couleur du color picker (sélecteur de couleur), et d'un rayon égal à la valeur définit dans le champs de sélection dans un intervalle.</p>

<pre class="brush: js">function draw() {
  if(pressed) {
    ctx.fillStyle = colorPicker.value;
    ctx.beginPath();
    ctx.arc(curX, curY-85, sizePicker.value, degToRad(0), degToRad(360), false);
    ctx.fill();
  }

  requestAnimationFrame(draw);
}

draw();</pre>

<div class="note">
<p><strong>Note :</strong> Les types d'{{htmlelement("input")}} <code>range</code> et <code>color</code> sont relativement bien pris en charge parmi les différents navigateurs, à l'exception des versions d'Internet Explorer inférieures à 10; et Safari ne prend pas en charge le type <code>color</code>. Si votre navigateur ne prend pas en charge ces types, il affichera simplement un champ texte et vous n'aurez qu'à entrer des valeurs de couleur et numéro valides vous-mêmes.</p>
</div>

<h2 id="WebGL">WebGL</h2>

<p>Il est maintenant temps de laisser la 2D derrière, et de jeter un coup d'oeil au canvas 3D. Le contenu 3D d'un canvas est spécifié en utilisant l'<a href="/fr/Apprendre/WebGL">API WebGL</a>, qui est une API complètement séparée de l'API des canvas 2D, même si ls deux sont affichés sur des éléments {{htmlelement("canvas")}}.</p>

<p>WebGL est basé sur le langage de programmation graphique <a href="/fr/docs/Glossaire/OpenGL">OpenGL</a>, et permet de communiquer directement avec le <a href="/fr/docs/Glossaire/GPU">GPU</a> de l'ordinateur. En soi, l'écriture WebGL est plus proche des langages de bas niveau tel que C++ que du JavaScript usuel; c'est assez complexe mais incroyablement puissant.</p>

<h3 id="Utiliser_une_bibliothèque">Utiliser une bibliothèque</h3>

<p>De par sa complexité, la plupart des gens écrivent du code de graphique 3D en utilisant une bibliothèque JavaScript tierce telle que <a href="/fr/docs/Games/Techniques/3D_on_the_web/Building_up_a_basic_demo_with_Three.js">Three.js</a>, <a href="/fr/docs/Games/Techniques/3D_on_the_web/Building_up_a_basic_demo_with_PlayCanvas">PlayCanvas</a> ou <a href="/fr/docs/Games/Techniques/3D_on_the_web/Building_up_a_basic_demo_with_Babylon.js">Babylon.js</a>. La plupart d'entre elles fonctionnent d'une manière similaire, offrant des fonctionnalités pour créer des formes primitives et personnalisées, positionner des caméras et des éclairages, recouvrir des surfaces avec des textures et plus encore. Elles se chargent de WebGL pour vous, vous permettant de travailler à un niveau plus haut.</p>

<p>Oui, en utiliser une signifie apprendre une autre nouvelle API (une API tierce en l'occurence), mais elles sont beaucoup plus simples que de coder du WebGL brut.</p>

<h3 id="Recréer_notre_cube">Recréer notre cube</h3>

<p>Regardons un exemple simple pour créer quelque chose avec une bibliothèque WebGL. Nous allons choisir <a href="/fr/docs/Games/Techniques/3D_on_the_web/Building_up_a_basic_demo_with_Three.js">Three.js</a>, puisque c'est l'une des plus populaires. Dans ce tutoriel, nous allons créer le cube 3D qui tourne que nous avons plus tôt.</p>

<ol>
 <li>
  <p>Pour commencer, créez une copie locale de <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/threejs-cube/index.html">index.html</a> dans un nouveau répertoire, et sauvegardez <a href="https://github.com/mdn/learning-area/blob/master/javascript/apis/drawing-graphics/threejs-cube/metal003.png">metal003.png</a> dans ce même répertoire. C'est l'image que nous allons utiliser comme texture de surface du cube plus tard.</p>
 </li>
 <li>
  <p>Ensuite, créez un nouveau fichier <code>main.js</code>, toujours dans le même répertoire.</p>
 </li>
 <li>
  <p>Si vous ouvrez <code>index.html</code> dans votre éditeur de texte, vous verrez qu'il y a deux éléments {{htmlelement("script")}} — le premier ajoute <code>three.min.js</code> à la page, et le second ajoute notre fichier <code>main.js</code> à la page. Vous devez <a href="https://raw.githubusercontent.com/mrdoob/three.js/dev/build/three.min.js">télécharger la bibliothèque three.min.js</a> et la sauvegarder dans le même répertoire que précédemment.</p>
 </li>
 <li>
  <p>Maintenant que nous avons inclus <code>three.js</code> dans notre page, nous pouvons commencer à écrire du code JavaScript qui l'utilise dans <code>main.js</code>. Commençons par créer une nouvelle scène — ajoutez ce qui suit dans le fichier <code>main.js</code>:</p>

  <pre class="brush: js">var scene = new THREE.Scene();</pre>

  <p>Le constructeur <code><a href="https://threejs.org/docs/index.html#api/scenes/Scene">Scene()</a></code> crée une nouvelle scène, qui représente l'ensemble du monde 3D que nous essayons d'afficher.</p>
 </li>
 <li>
  <p>Ensuite, nous avons besoin d'une <strong>caméra</strong> pour voir la scène. En terme d'imagerie 3D, la caméra représente la position du spectateur dans le monde. Pour ajouter une caméra, ajoutez les lignes suivantes à la suite:</p>

  <pre class="brush: js">var camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
camera.position.z = 5;
</pre>

  <p>Le constructeur <code><a href="https://threejs.org/docs/index.html#api/cameras/PerspectiveCamera">PerspectiveCamera()</a></code> prend quatre arguments:</p>

  <ul>
   <li>Le champ de vision: Quelle est la largeur de la zone devant la caméra qui doit être visible à l'écran, en degrés.</li>
   <li>Le rapport d'aspect (aspect ratio): Habituellement, c'est le rapport entre la largeur de la scène divisé par la hauteur de la scène. Utiliser une autre valeur va déformer la scène (ce qui pourrait être ce que vous voulez, mais ce n'est généralement pas le cas).</li>
   <li>Le plan proche (near plane): Jusqu'où les objets peuvent être proches de la caméra avant que nous arrêtions de les afficher à l'écran. Pensez-y comme quand vous approchez votre doigt de plus en plus près de l'espace entre vos yeux, vous finissez par ne plus le voir.</li>
   <li>Le plan éloigné (far plane): Jusqu'à quelle distance de la caméra doit-on afficher les objets.</li>
  </ul>

  <p>Nous définissons également la position de la caméra à 5 unités de distance de l'axe Z, qui, comme en CSS, est hors de l'écran vers vous, le spectateur.</p>
 </li>
 <li>
  <p>Le troisième ingrédient essentiel est un moteur de rendu. C'est un objet qui restitue une scène donnée, vu à travers une caméra donnée. Nous allons en créer dès à présent en utilisant le constructeur <code><a href="https://threejs.org/docs/index.html#api/renderers/WebGLRenderer">WebGLRenderer()</a></code> — mais nous ne l'utiliserons que plus tard. Ajoutez les lignes suivantes à la suite de votre JavaScript:</p>

  <pre class="brush: js">var renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);</pre>

  <p>La première ligne crée un nouveau moteur de rendu, la deuxième ligne définit la taille à laquelle le moteur de rendu va dessiner la vue de la caméra, et la troisième ligne ajoute l'élément {{htmlelement("canvas")}} crée par le moteur de rendu au {{htmlelement("body")}} du document. Désormais, tout ce que dessine le moteur de rendu sera affiché dans notre fenêtre.</p>
 </li>
 <li>
  <p>Ensuite, nous voulons créer le cube que nous afficherons sur le canvas. Ajoutez le morceau de code suivant au bas de votre JavaScript:</p>

  <pre class="brush: js">var cube;

var loader = new THREE.TextureLoader();

loader.load( 'metal003.png', function (texture) {
  texture.wrapS = THREE.RepeatWrapping;
  texture.wrapT = THREE.RepeatWrapping;
  texture.repeat.set(2, 2);

  var geometry = new THREE.BoxGeometry(2.4, 2.4, 2.4);
  var material = new THREE.MeshLambertMaterial( { map: texture, shading: THREE.FlatShading } );
  cube = new THREE.Mesh(geometry, material);
  scene.add(cube);

  draw();
});</pre>

  <p>Il y a un peu plus à encaisser ici, alors allons-ici par étapes:</p>

  <ul>
   <li>Nous créons d'abord une variable globale <code>cube</code> pour pouvoir accéder à notre cube de n'importe où dans notre code.</li>
   <li>Ensuite, nous créons un nouvel objet <code><a href="https://threejs.org/docs/index.html#api/loaders/TextureLoader">TextureLoader</a></code>, et appellons <code>load()</code> dessus. La fonction <code>load()</code> prend deux paramètres dans notre exemple (bien qu'elle puisse en prendre plus): la texture que nous voulons charger (notre PNG), et la fonction qui sera exécutée lorsque la texture sera chargée.</li>
   <li>À l'intérieur de cette fonction, nous utilisons les propriétés de l'objet <code><a href="https://threejs.org/docs/index.html#api/textures/Texture">texture</a></code> pour spécifier que nous voulons une répétition 2 x 2 de l'image sur tous les côtés du cube.</li>
   <li>Ensuite, nous créons un nouvel objet <code><a href="https://threejs.org/docs/index.html#api/geometries/BoxGeometry">BoxGeometry</a></code> et <code><a href="https://threejs.org/docs/index.html#api/materials/MeshLambertMaterial">MeshLambertMaterial</a></code>, que nous passons à un <code><a href="https://threejs.org/docs/index.html#api/objects/Mesh">Mesh</a></code> pour créer notre cube. Typiquement, un objet requiert une géométrie (quelle est sa forme) et un matériau (à quoi ressemble sa surface).</li>
   <li>Pour finir, nous ajoutons notre cube à la scène, puis appellons la fonction <code>draw()</code> pour commencer l'animation.</li>
  </ul>
 </li>
 <li>
  <p>Avant de définir la fonction <code>draw()</code>, nous allons ajouter quelques lumières à la scène, pour égayer un peu les choses; ajoutez le bloc suivant à la suite de votre code:</p>

  <pre class="brush: js">var light = new THREE.AmbientLight('rgb(255, 255, 255)'); // soft white light
scene.add(light);

var spotLight = new THREE.SpotLight('rgb(255, 255, 255)');
spotLight.position.set( 100, 1000, 1000 );
spotLight.castShadow = true;
scene.add(spotLight);</pre>

  <p>Un objet <code><a href="https://threejs.org/docs/index.html#api/lights/AmbientLight">AmbientLight</a></code> est une lumière douce qui illumine la scène entière, un peu comme le soleil comme vous êtes dehors. Un objet <code><a href="https://threejs.org/docs/index.html#api/lights/AmbientLight">SpotLight</a></code>, d'autre part, est un faisceau de lumière, plutôt comme une lampe de poche/torche (ou un spotlight - projecteur - en fait).</p>
 </li>
 <li>
  <p>Pour finir, ajoutons notre fonction <code>draw()</code> au bas du code:</p>

  <pre class="brush: js">function draw() {
  cube.rotation.x += 0.01;
  cube.rotation.y += 0.01;
  renderer.render(scene, camera);

  requestAnimationFrame(draw);
}</pre>

  <p>C'est assez intuittif: sur chaque image, on fait légèrement tourner notre cube sur ses axes X et Y, affichons la scène telle qu'elle vue par notre caméra, puis appellons <code>requestAnimationFrame()</code> pour planifier le dessin de notre prochaine image.</p>
 </li>
</ol>

<p>Jetons un coup d'oeil rapide au produit fini:</p>

<p>{{EmbedGHLiveSample("learning-area/javascript/apis/drawing-graphics/threejs-cube/index.html", '100%', 500)}}</p>

<p>Vous pouvez <a href="https://github.com/mdn/learning-area/tree/master/javascript/apis/drawing-graphics/threejs-cube">trouver le code terminé sur GitHub</a>.</p>

<div class="note">
<p><strong>Note :</strong> Dans notre repo GitHub vous pouvez également trouver d'autres exemples 3D intéressants — <a href="https://github.com/mdn/learning-area/tree/master/javascript/apis/drawing-graphics/threejs-video-cube">Three.js Video Cube</a> (<a href="https://mdn.github.io/learning-area/javascript/apis/drawing-graphics/threejs-video-cube/">le voir en direct</a>). On utilise {{domxref("MediaDevices.getUserMedia", "getUserMedia()")}} pour prendre un flux vidéo à partir d'une webcam de l'ordinateur et le projetons sur le côté du cube comme texture!</p>
</div>

<h2 id="Sommaire">Sommaire</h2>

<p>À ce stade, vous devriez avoir une idée utile des bases de la programmation graphique en utilisant Canvas et WebGL et de ce que vous pouvez faire avec ces APIs. Vous pouvez trouver des endroits où aller pour trouver plus d'informations dans la section suivante. Amusez-vous!</p>

<h2 id="Voir_aussi">Voir aussi</h2>

<p>Nous n'avons couverts dans cet article que les vraies bases du canvas — il y a tellement plus à apprendre! Les articles suivants vous mèneront plus loin.</p>

<ul>
 <li><a href="/fr/docs/Tutoriel_canvas">Tutoriel canvas</a> — Une série de tutoriels très détaillés qui explique ce que vous devriez savoir à propos du canvas 2D de manière beaucoup plus poussée qu'ici. Lecture indispensable.</li>
 <li><a href="/fr/docs/Web/API/WebGL_API/Tutorial">Tutoriel WebGL</a> — Une série de tutoriels qui enseigne les bases de la programmation WebGL brute.</li>
 <li><a href="/fr/docs/Games/Techniques/3D_on_the_web/Building_up_a_basic_demo_with_Three.js">Construire une démo basique avec Three.js</a> — tutoriel Three.js basique. Nous avons également les guides équivalents pour <a href="/fr/docs/Games/Techniques/3D_on_the_web/Building_up_a_basic_demo_with_PlayCanvas">PlayCanvas</a> et <a href="/fr/docs/Games/Techniques/3D_on_the_web/Building_up_a_basic_demo_with_Babylon.js">Babylon.js</a>.</li>
 <li><a href="/fr/docs/Jeux">Développement de jeux vidéos</a> — La page d'atterrisage sur MDN pour le développement de jeux web. Il y a quelques tutoriels et techniques disponibles liés au canvas 2D et 3D — voir les options du menu Techniques et Tutoriels.</li>
</ul>

<h2 id="Exemples">Exemples</h2>

<ul>
 <li><a href="https://github.com/mdn/violent-theremin">Violent theramin</a> — Utilise l'API Web Audio pour générer des sons, et Canvas pour générer une visualisation.</li>
 <li><a href="https://github.com/mdn/voice-change-o-matic">Voice change-o-matic</a> — Utilise un canvas pour visualiser en temps réel les données audio de l'API Web Audio.</li>
</ul>

<p>{{PreviousMenuNext("Learn/JavaScript/Client-side_web_APIs/Third_party_APIs", "Learn/JavaScript/Client-side_web_APIs/Video_and_audio_APIs", "Learn/JavaScript/Client-side_web_APIs")}}</p>

<p> </p>

<h2 id="Dans_ce_module">Dans ce module</h2>

<ul>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Introduction">Introduction aux API du Web</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Manipulating_documents">Manipuler des documents</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Fetching_data">Récupérer des données du serveur</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Third_party_APIs">APIs tierces</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Drawing_graphics">Dessiner des éléments graphiques</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Video_and_audio_APIs">APIs vidéo et audio</a></li>
 <li><a href="/fr/Apprendre/JavaScript/Client-side_web_APIs/Client-side_storage">Stockage côté client</a></li>
</ul>