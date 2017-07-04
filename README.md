# Seminar 9

## Semantisches HTML statt nur "`divs`"

Semantik laut Duden: Bedeutung, Inhalt (eines Wortes, Satzes oder Textes)

HTML5 bietet HTML Tags, welche die Semantik eines Dokuments wiederspiegeln.

Also anstatt:

```html
<!DOCTYPE html>
<html>
<head>
 	<meta charset="utf-8">
	<title>Willkommen</title>
</head>
<body>
    <div class="header">Willkommen zu meiner Homepage</div>
    <div class="nav">
        <ul>
            <li><a href="index.html">Home</a></li>
            <li><a href="produkte.html">Produkte</a></li>
            <li><a href="ueber_uns.html">Über uns</a></li>
            <li><a href="kontakt.html">Kontakt</a></li>
        </ul>
    </div>
    <div class="main">
        Lorem ipsum dolor usw. und so fort bis der Blindtext nicht mehr weiter weiss. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.
    </div>
    <div class="aside">
        Das ist der nebendran text. Den man in einer weiteren Spalte sehen könnte und wo man irgendwelches Zeug reinschreibt.
    </div>    
    <div class="footer">
        <p>Copyright 2017</p>
        <ul>
            <li><a href="impressum.html">Impressum</a></li>
            <li><a href="datenschutz.html">Datenschutz</a></li>
        </ul>
    </div>
</body>
</html>
```
> ungestylt_unsemantisch.html

Würde man heute eher so etwas schreiben wollen:

```html
<!DOCTYPE html>
<html>
<head>
 	<meta charset="utf-8">
	<title>Willkommen</title>
</head>
<body>
    <header>Willkommen zu meiner Homepage</header>
    <nav>
        <ul>
            <li><a href="index.html">Home</a></li>
            <li><a href="produkte.html">Produkte</a></li>
            <li><a href="ueber_uns.html">Über uns</a></li>
            <li><a href="kontakt.html">Kontakt</a></li>
        </ul>
    </nav>
    <section id="main">
        Lorem ipsum dolor usw. und so fort bis der Blindtext nicht mehr weiter weiss. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.
    </section>
    <aside>
        Das ist der nebendran text. Den man in einer weiteren Spalte sehen könnte und wo man irgendwelches Zeug reinschreibt.
    </aside>
    <footer>
        <p>Copyright 2017</p>
        <ul>
            <li><a href="impressum.html">Impressum</a></li>
            <li><a href="datenschutz.html">Datenschutz</a></li>
        </ul>
    </footer>
</body>
</html>
```
> ungestylt_semantisch.html

Siehe hier https://www.w3.org/wiki/HTML_structural_elements#Introduction

### Styling - `section` und `aside` nebeneinander 

Das Styling mit CSS kann dann direkt auf die Elemente erfolgen statt auf die 
Klassen, die den `div` tags zugeordnet sind. 

Siehe `gestylt_semantisch1.html` und `mystyle1.css`

```css
header,
section,
aside,
footer {
  /* Margin gilt für oben, rechts, unten, links https://developer.mozilla.org/de/docs/Web/CSS/margin 
     Margin ist der Rand ausserhalb des des Borders
     Also von aussen nach innen Margin, Border, Padding - Padding der Rand innerhalb des Borders
     Prozent bezieht sich auf die Breite des containers der das ganze beinhaltet (also Body in diesen Fällen)
     Siehe try.html und try.css für exakten Beweis
  */
  margin: 0 1% 24px 1%; 
}
section {
  /* float:left sorgt dafür, dass die Sektion links "schwimmt" und 63% des Platzes einnimmt  
     float bedeutet grundsätzlich, dass ein Element nicht dem normalen Fluss einer Seite folgt sondern es
     in diesem Fall links zu seinem Eltern Element (body in diesem Fall) positioniert wird. Alle anderen
     Elemente "floaten" jetzt um das Element herum. 
     Bei einem Bild wie eine <img> Tag würde der Text um das Bild herum gehen. Wenn wir mehrere
     Elemente haben die "schwimmen" kann man so verursachen, dass die Elemente nebeneinander in Spalten stehen.
  */
  float: left;
  /* Die Grössenangabe ist hier wichtig. Sonst würde das Element den Platz einnehmen gemäss Inhalt. der ist
     recht viel und damit würde die Sektion wieder den ganzen Platz einnehmen. Oder wenn es nur ganz wenig
     inhalt hätte würde es ziemlich schmall sein */
  width: 63%;
}
aside {
  /* float:right sorgt dafür, dass der Absatz rechts "schwimmt" und 30% des Platzes einnimmt  */
  float: right;
  /* Ditto zu section ist die Breite wichtig anzugeben, da sonst die Breite vom Inhalt abhängig ist */
  width: 30%;
}
footer {
  /* Aber den Footer wollen wir nicht unter dem "aside" haben, mit clear: both löst man das "schwimmen" wieder auf
     Footer würde ohne dem unter dem aside platziert werden, weil dort Platz ist. Oder unter section wenn dort Platz wäre.
     oder wenn man die Breite geringer machen würden in der Mitte dazwischen. Mit clear:both verursacht man, dass der Footer
     wirklich unter den zwei schwimmenden Elementen sitzt.
     http://stackoverflow.com/a/27082817/382009 */
  clear: both;
  margin-bottom: 0;
}
```

Es lohnt sich ein wenig herumzuspielen um zu sehen wie das alles funktioniert. Als Erinnerung
CSS Selektoren `#` für die ID des Tags `.` für Class und ohne alles für das gesamte Tag.

### Styling `nav` mit Menüpunkte nebeneinander

Funktioniert ähnlich:

Siehe `mystyle2.css`

```CSS
header,
section,
aside,
footer {
  margin: 0 1.5% 24px 1.5%;
}
nav {
  /* Die Nav Bar wollen wir auch floaten aber sie soll den ganzen Platz einnehmen,
     damit die folgenden Floating Elemente auf der nächsten "Zeile" anfangen*/
  float: left;
  width: 100%;
}
nav > ul > li {
  /* Innerhalb von nav sollen die Listenelemente auch nebeneinander sein*/
  float: left;
  margin: 0 2% 24px 2%;
}
section {
  float: left;
  width: 63%;
}
aside {
  float: right;
  width: 30%;
}
footer {
  clear: both;
  margin-bottom: 0;
}
```

### Styling mit Clearfix

Der Wechsel zwischen "Normal" und "Float" ist bedeutend.

`header` umfasst auch die Navigationbar und erhält die Clearfix Klasse. `section` 
und `aside` werden in ein `div` gewrappt um die `clearfix` Klasse zuzordnen. 

Siehe `gestylt_semantisch3.html` und `mystyle3.css`

```html
<!DOCTYPE html>
<html>
<head>
 	<meta charset="utf-8">
	<title>Willkommen</title>
	<link rel="stylesheet" type="text/css" href="mystyle3.css">
</head>
<body>
    <header class="clearfix">
        Willkommen zu meiner Homepage
        <nav>
            <ul>
                <li><a href="index.html">Home</a></li>
                <li><a href="produkte.html">Produkte</a></li>
                <li><a href="ueber_uns.html">Über uns</a></li>
                <li><a href="kontakt.html">Kontakt</a></li>
            </ul>
        </nav>
    </header>
    <div class="clearfix">
        <section>
            Lorem ipsum dolor usw. und so fort bis der Blindtext nicht mehr weiter weiss. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.
        </section>
        <aside>
            Das ist der nebendran text. Den man in einer weiteren Spalte sehen könnte und wo man irgendwelches Zeug reinschreibt.
        </aside>
    </div>
    <footer>
        <p>Copyright 2017</p>
        <ul>
            <li><a href="impressum.html">Impressum</a></li>
            <li><a href="datenschutz.html">Datenschutz</a></li>
        </ul>
    </footer>
</body>
</html>
```

Im CSS kann jetzt Clearfix definiert werden.

```CSS
header,
section,
aside,
footer {
  margin: 0 1.5% 24px 1.5%;
}
nav > ul > li {
  /* Innerhalb von nav sollen die Listenelemente auch nebeneinander sein*/
  float: left;
  margin: 0 2% 0 2%;
}
section {
  float: left;
  width: 63%;
}
aside {
  float: right;
  width: 30%;
}
footer {
  margin-bottom: 0;
}

/* :before und :after sind pseudo-elemente mit denen man Styling davor und danach angeben kann 
   Das folgende wird "Clearfix" genannt. Es gibt davon viele Versionen davon im Netz, besonders
   wenn frühere Browser unterstützt werden müssen und die waren lange und kompliziert.
   https://css-tricks.com/snippets/css/clear-fix/
   Man bräuchte auch eine :before Aber wenn man die Navigation als Teil des Headers ansieht und
   diesem dann die clearfix Klasse gibt, erreichen wir was wir wollen
*/
.clearfix:after {
  content: "";
  display: table;
  clear: both;
}
```

### Styling mit `inline-block`

Neben `float` kann auch das Attribut `display` auf `inline-block` gesetzt werden.

Siehe `mystyle4.css`

```CSS
header,
section,
aside,
footer {
  margin: 0 1.5% 24px 1.5%;
}
nav > ul > li {
  float: left;
  margin: 0 2% 0 2%;
}
section {
  /* Inline-Block funktioniert auch um Section und Aside nebeneneinander zu bekommen */
  display: inline-block;
  width: 63%;
  /* Jetzt benötigt es aber dies, weil sonst wird die jeweils kleinere Spalte von unten ab angezeigt */
  vertical-align: top;
}
aside {
  /* Hier entsprechend auch*/
  display: inline-block;
  width: 30%;
  vertical-align: top;
}
footer {
  margin-bottom: 0;
}

.clearfix:after {
  content: "";
  display: table;
  clear: both;
}
```

### Responsive Styling

Mit `@media print` und `@media screen` kann man Styling einschränken. Dort kann
man mit `and (min-width: 420px)` angeben ab welcher Breite das Styling überhaupt
angewendet wird.

Siehe `mystyle5.css`

```css
header,
section,
aside,
footer {
  margin: 0 1.5% 24px 1.5%;
}
nav > ul > li {
  float: left;
  margin: 0 2% 0 2%;
}
/* Gilt immer */
section, aside {
  vertical-align: top;
}
/* Gilt bei schmall */
@media all and (min-width: 420px) {
  section, aside {
    display: inline-block;
  }
  section {
    width: 63%;
  }
  aside {
    display: inline-block;
    width: 27%;
  }
}
footer {
  margin-bottom: 0;
}

.clearfix:after {
  content: "";
  display: table;
  clear: both;
}
```
## SASS

Das ist eine über CSS gestülpte Sprache. SASS ist schon vorinstalliert. Damit
Dateien vom type `SCSS` automatisch in `CSS` umgewandelt werden muss im 
Terminal ein "Watcher" laufen:

```bash
hol42:~/workspace (master) $ sass --watch css
```

Es wird auch immer eine `.css.map` erstellt. Die Chrome Developer Tools lesen
diese Map Files. Sie sind nur `JSON` formatierte Dateien und erlauben es so, 
statt CSS direkt SCSS in den Developer Tools zu sehen.

Experimente laufen mit `sass_1.html`

```html
<!DOCTYPE html>
<html>
<head>
 	<meta charset="utf-8">
	<title>Willkommen</title>
	<link rel="stylesheet" type="text/css" href="css/sass_1.css">
    <meta name="viewport" content="width=device-width">
</head>
<body>
    <header class="clearfix">
        <div class="welcome">Willkommen zu meiner Homepage</div><!-- 
         
        --><div class="menu">
            <nav>
                <ul>
                    <li><a href="index.html">Home</a></li>
                    <li><a href="produkte.html">Produkte</a></li>
                    <li><a href="ueber_uns.html">Über uns</a></li>
                    <li><a href="kontakt.html">Kontakt</a></li>
                </ul>
            </nav>
        </div>
    </header>
    <div class="clearfix">
        <section>
            Lorem ipsum dolor usw. und so fort bis der Blindtext nicht mehr weiter weiss. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.
        </section><aside>
            Das ist der nebendran text. Den man in einer weiteren Spalte sehen könnte und wo man irgendwelches Zeug reinschreibt.
        </aside>
    </div>
    <footer>
        <p>Copyright 2017</p>
        <ul>
            <li><a href="impressum.html">Impressum</a></li>
            <li><a href="datenschutz.html">Datenschutz</a></li>
        </ul>
    </footer>
</body>
</html>
```

Es gibt verschiedene sinnvolle Sprachelemente, die einem das Leben mit CSS
etwas erleichtert:

```SCSS
@import 'reset';
@import 'useful';
@import 'mycolors';
@import 'font-families';

$font-family: $font-avant-garde;

body {
  font-family: $font-family;
  color: $main; 
  background-color: $background-color;
}

header {
  .welcome {
    float: left;
    font-weight: bold;
  }
  .menu {
    float: right;
    nav {
      ul {
        margin: 0;
        padding: 0;
        list-style: none;
      }
    
      li { 
        display: inline-block; 
        margin: 0.25em;
      }
    }
  }
}
header,
section,
aside,
footer {
  margin: 0 1.5% 24px 1.5%;
}
/* Gilt immer */
section, aside {
  vertical-align: top;
}
/* Gilt bei schmall */
@media all and (min-width: 420px) {
  section, aside {
    display: inline-block;
  }
  section {
    width: (2/3) * 90%;
  }
  aside {
    width: (1/3) * 90%;
  }
}
footer {
  margin-bottom: 0;
  li { 
    margin-left: 1em;
  }
}
```

Was ist hier sinnvolles passiert

- Sachen die man immer wieder braucht kann man in `@imports` auslagern.
- Variablen für die Font-Familien
- Verschachtelte (Nested) Selektoren
- Berechnungen, z.B. (2/3) * 90%

Es gibt noch einiges mehr: http://sass-lang.com/guide

## Flexbox

Float ist eigentlich schon längst wieder out und war auch eigentlich wirklich
nur für das einpassen von Bildern im Fluss eines Textes. Siehe Beispiel:
https://css-tricks.com/all-about-floats/

Es ist somit ein Hack. Punkt.

Danach kam Flexbox und jetzt neu gibt es CSS Grid. Beide zusammen bieten
ihre Möglichkeiten. CSS Grid funktioniert nur auf den neuesten Browser
Versionen.

Siehe `flex.html` und `flex.css` wie unser Layout gestylt werden kann:

```HTML
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Willkommen</title>
    <link rel="stylesheet" type="text/css" href="flex.css">
    <meta name="viewport" content="width=device-width">
</head>
<body>
<header class="clearfix">
    Willkommen zu meiner Homepage
</header>
<nav>
    <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="produkte.html">Produkte</a></li>
        <li><a href="ueber_uns.html">Über uns</a></li>
        <li><a href="kontakt.html">Kontakt</a></li>
    </ul>
</nav>
<div class="main">
    <section>
        Lorem ipsum dolor usw. und so fort bis der Blindtext nicht mehr weiter weiss. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.
    </section>
    <aside>
        Das ist der nebendran text. Den man in einer weiteren Spalte sehen könnte und wo man irgendwelches Zeug reinschreibt.
    </aside>
</div>
<footer>
    <p>Copyright 2017</p>
    <ul>
        <li><a href="impressum.html">Impressum</a></li>
        <li><a href="datenschutz.html">Datenschutz</a></li>
    </ul>
</footer>
</body>
</html>
```

```CSS
.main {
    display: flex;
    flex-flow: row;
}
section {
    flex: 70%;
    order: 1;
}
aside {
    flex: 30%;
    order: 2;
}
nav > ul > li {
    display: inline-block;
}
```

Der Bereich der von `section` und `aside` wird in der `div` mit Klasse `.main`
gesteckt. 

Klasse `.main` wird dann unter Kontrolle von Flexbox gestellt mit `display: flex`.
Der Flow wird auf `row` gestellt, dazu gleich noch mehr.

Die Kinder-Element `section` und `aside` erhalten 70% bzw. 30% und werden angeordnet. 
Man kann mit der `order` ganz leicht also die zwei vertauschen.

Das Menü wurde einfach mit in `inline-block` nebeneinander gestellt.

Auf dieser Seite kann sehr gut gezeigt werden was die Möglichkeiten von
Flexbox sind und wie es viele Problem löst. Heute kann man davon ausgehen,
dass alle Browser Flexbox beherrschen: http://the-echoplex.net/flexyboxes/


# CSS Grid

Leider können nur die neuesten Versionen Browser CSS Grid. So kann 
es die Version 52 des Chrome Browsers vom Juli 2016 nicht. Es gibt
dafür ein Polyfill (Polyfills sind JS Routinen, die älteren Browsern features
von neueren Browsern beibringen). Im Beispiel ist

```HTML
<script src="css-polyfills.min.js"></script>
```

enthalten. Das hierher kommt: https://github.com/FremyCompany/css-grid-polyfill

Zu Grid gibt es viele gute Einführungswebseiten. Diese fand ich persönliche
am verständlichsten, neben der offiziellen W3C Doku:

https://www.quackit.com/css/grid/tutorial/create_a_website_layout.cfm

https://www.w3.org/TR/css-grid-1/#intro

Hier das Beispiel. Zuerst der HTML Code von `grid.html`

```HTML
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Willkommen</title>
    <link rel="stylesheet" type="text/css" href="grid.css">
    <meta name="viewport" content="width=device-width">
</head>
<body>
<header class="clearfix">
    Willkommen zu meiner Homepage
</header>
<nav>
    <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="produkte.html">Produkte</a></li>
        <li><a href="ueber_uns.html">Über uns</a></li>
        <li><a href="kontakt.html">Kontakt</a></li>
    </ul>
</nav>
<section>
    Lorem ipsum dolor usw. und so fort bis der Blindtext nicht mehr weiter weiss. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.
</section>
<aside>
    Das ist der nebendran text. Den man in einer weiteren Spalte sehen könnte und wo man irgendwelches Zeug reinschreibt.
</aside>
<footer>
    <p>Copyright 2017</p>
    <ul>
        <li><a href="impressum.html">Impressum</a></li>
        <li><a href="datenschutz.html">Datenschutz</a></li>
    </ul>
</footer>
<script src="css-polyfills.min.js"></script>
</body>
</html>
```

Dazu das `grid.css`

```CSS
body {
    display: grid;
    grid-template-areas:
            "header header "
            "nav nav"
            "section aside"
            "footer footer";
    grid-template-columns: 70% 30%;
    grid-gap: 10px;
}
header {
    grid-area: header;
}
nav {
    grid-area: nav;
}
nav > ul > li {
    display: inline-block;
}
section {
    grid-area: section;
}
aside {
    grid-area: aside;
}
footer {
    grid-area: footer;
}
```

Für den gesamten Body wird mit `display: grid` auf Grid CSS Modus umgeschaltet.
Die Grid Areas werden angordnet, wobei man einfach das Element wiederholt, wenn
man es über zwei Spalten hinweg benötigt (`grid-template-areas`).

die Spaltengrössen werden festgelegt (`grid-template-columns`), der Platz dazwischen
wird mit `grid-gap` bestimmt. 

Dansch werden einfach die einzelnen Elemente benennt. Zur Einfachheit habe ich die 
Grid Elemente gleich genannt, das könnte aber auch verwirrend sein.

# Holy Grail Layout

Das ist das übliche Layout von oben Header, mitte 3 Spaltig, unten Footer.

Siehe `grid2.html` (identisch) und `grid2.css`

```HTML
body {
    display: grid;
    grid-template-areas:
            "header header header "
            "nav section aside"
            "footer footer footer";
    grid-template-columns: 20% 50% 30%;
    grid-gap: 10px;
}
header {
    grid-area: header;
}
nav {
    grid-area: nav;
}
section {
    grid-area: section;
}
aside {
    grid-area: aside;
}
footer {
    grid-area: footer;
}
```





