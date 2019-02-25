# Frontend style guide
Deze guide beschrijft algemene richtlijnen voor frontend development (html, css, js).

## Algemeen
- Absolute url's zonder domeinnaam voor: Afbeeldingen, stylesheets, javascript, achtergrond-afbeeldingen, ect.
- Gebruik geen* id's! <sub><sup>Er zijn enkele uitzonderingen. Bijvoorbeeld gegenereerde id's en specifieke elementen voor javascipt.</sup></sub>

## CSS
**Index**
- Algemeen
- Benamingen
- Volgorde
- Uitlijnen
- Single-responsibility classes
- Blokken met media queries
- Gebruik van !important

**Algemeen**
## kabab-case
Alle id's en classes in kabab-case (tenzij je BEM gebruikt).

❌ **Fout:**
```
<ul class="mainmenu"></ul>
<ul class="mainMenu"></ul>
<ul class="MainMenu"></ul>
<ul class="main_menu"></ul>
<ul class="main_Menu"></ul>
<ul class="Main_Menu"></ul>
```

✔ **Goed:**
```
<ul class="main-menu"></ul>
```
## Recycelen
❌ **Niet:** recycelen als de eigenschappen toevallig overeen komen. 
```
.main-menu__item,
.contact-form {
	margin-right: 20px;
	border-bottom: 2px solid blue;
}

.contact-form{
	margin-left: 20px;
}
```
_In dit geval komen de gewenste properties toevallig overeen. Dan moeten ze gewoon los worden geschreven._

✔ **Wel:** recycelen als de gehele selector hetzelfde doel heeft.
```
.button-container a,
.button-container button {
	background-color: #3333ff;
}
```
```
.main-slider,
.content-row {
	margin-bottom: 30px;
}
```
_In deze gevallen komen de properties om een reden overeen. Als er een property moet worden aangepast mogen ze op beide locaties wijzigen._

## Volgorde
Probeer in globale lijnen de volgorde van het document aan te houden. Liever 2x declareren dan een onduidelijk document. 
Site- en document algemene declaraties bovenin het bestand. Groeperen met comments mag. 

✔ **Goed:**
```
== GENERAL ==
	.button {
		...
	}

== HOME SLIDER ==
	.slider {
		...
	}

	.slider__slide {
		...
	}
```

## Uitlijnen
❌ **Fout:**
```
.main-menu 
{
	background-color: white;
	color: black;
}
```
```
.main-menu {
background-color: white;
color: black;
}
```
```
.main-menu { background-color: white; color: black; }
```

✔ **Goed:**
```
.main-menu {
	color: black;
	background-color: white;
}
```

In enkele gevallen mogen declaraties op één regel. Bijvoorbeeld als er veel rulesets dezelfde properties hebben.

```
.cloud item {
	position: absolute;
}

.cloud item-1 { top: 10px; left: 30px; }
.cloud item-2 { top: 20px; left: 60px; }
.cloud item-3 { top: 30px; left: 90px; }
.cloud item-4 { top: 40px; left: 120px; }

```

## Single-responsibility classes
Het komt voor dat je modifiers gebruikt als class (✔). Maar gebruik deze alleen voor die modification! Daardoor kun je ze herbruiken.

❌ **Fout:**
```
.no-border {
	border: none;
	width: 300px;
}
```
```
.uppercase {
	text-transform: uppercase;
	font-weight: bold;
}
```

 **Goed:**
```
.hidden {
	display: none;
}
```
```
.no-border {
	border: none;
}
```
```
.uppercase {
	text-transform: uppercase;
}
```

## Blokken met media queries
Zet niet alle rulesets voor mobiel in één media query. De volgorde van het document is belangrijker. 


## (Optioneel) BEM [[1]](https://en.bem.info/methodology/quick-start/)[[2]](http://getbem.com/introduction/)[[3]](http://getbem.com/naming/)
`block-name__elem-name_mod-name_mod-val`

- Names are written in lowercase Latin letters.
- Words are separated by a hyphen (-).
- The block name defines the namespace for its elements and modifiers.
- The element name is separated from the block name by a double underscore (\_\_).
- The modifier name is separated from the block or element name by a single underscore (\_).
- The modifier value is separated from the modifier name by a single underscore (\_).
- For boolean modifiers, the value is not included in the name.

## Gebruik van important
Probeer `!important` te vermijden!

1. Werkt het als ik `!important` toevoeg?
2. Welke stylesheet/ruleset overschrijft de definitie die je probeerd toe te voegen?
3. Kan je selector specifieker?

Zie:
- [Cascade and inheritance](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Cascade_and_inheritance)
- [Specificity]https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity
- [Which CSS entities participate in the cascadeSection](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade)

### Block
✔ **Goed:**
```
<ul class="main-menu"></ul>
```

### Element
❌ **Fout:**
```
<li class="item"></li>
<li class="main-menu-item"></li>
```

✔ **Goed:**
```
<li class="main-menu__item"></li>
```

### Modifiers
❌ **Fout:**
```
<li class="main-menu__item active"></li>
<li class="main-menu__item-active"></li>
```

✔ **Goed:**
```
<li class="main-menu__item_active"></li>
<li class="main-menu__item_color_blue"></li>
```
