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

