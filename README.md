# Frontend style guide
Deze guide beschrijft algemene richtlijnen voor frontend development (html, css, js).

**Inhoud**
- [Algemeen](#algemeen)
- [kebab-case](#kebab-case)
- [Recycelen](#recycelen)
- [Volgorde](#volgorde)
- [Uitlijnen](#uitlijnen)
- [Single-responsibility classes](#single-responsibility-classes)
- [Media queries](#media-queries)
- [Gebruik van important](#gebruik-van-important)
- [(Optioneel) BEM](#optioneel-bem)

## Algemeen
- Absolute url's zonder domeinnaam voor: Afbeeldingen, stylesheets, javascript, achtergrond-afbeeldingen, ect.
- Gebruik geen* id's! <sup>* Er zijn enkele uitzonderingen. Bijvoorbeeld gegenereerde id's en javascipt gebruik.</sub>

❌ **Fout:**
```html
<img src="https://domain.com/about-us/images/my-image.png" />
<img src="images/my-image.png" />
```

✔ **Goed:**
```html
<img src="/about-us/images/my-image.png" />
```

## CSS
### kebab-case
Alle id's en classes in kebab-case (tenzij je BEM gebruikt).

❌ **Fout:**
```html
<ul class="mainmenu"></ul>
<ul class="mainMenu"></ul>
<ul class="MainMenu"></ul>
<ul class="main_menu"></ul>
<ul class="main_Menu"></ul>
<ul class="Main_Menu"></ul>
```

✔ **Goed:**
```html
<ul class="main-menu"></ul>
```

### Recycelen
❌ **Niet:** recycelen als de eigenschappen toevallig overeen komen. 
```css
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
```css
.button-container a,
.button-container button {
    background-color: #3333ff;
}
```
```css
.main-slider,
.content-row {
    margin-bottom: 30px;
}
```
_In deze gevallen komen de properties om een reden overeen. Als er een property moet worden aangepast mogen ze op beide locaties wijzigen._

### Volgorde
Probeer in globale lijnen de volgorde van het document aan te houden. Liever 2x declareren dan een onduidelijk document. 
Site- en document algemene declaraties bovenin het bestand. Groeperen met comments mag. 

✔ **Goed:**
```css
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

### Uitlijnen
❌ **Fout:**
```css
.main-menu 
{
    background-color: white;
    color: black;
}
```
```css
.main-menu {
background-color: white;
color: black;
}
```
```css
.main-menu { background-color: white; color: black; }
```

✔ **Goed:**
```css
.main-menu {
    color: black;
    background-color: white;
}
```

In enkele gevallen mogen declaraties op één regel. Bijvoorbeeld als er veel rulesets dezelfde properties hebben.

```css
.cloud item {
    position: absolute;
}

.cloud item-1 { top: 10px; left: 30px; }
.cloud item-2 { top: 20px; left: 60px; }
.cloud item-3 { top: 30px; left: 90px; }
.cloud item-4 { top: 40px; left: 120px; }
```

### Single-responsibility classes
Het komt voor dat je modifiers gebruikt als class (✔). Maar gebruik deze alleen voor die modification! Daardoor kun je ze herbruiken.

❌ **Fout:**
```css
.no-border {
    border: none;
    width: 300px;
}
```
```css
.uppercase {
    text-transform: uppercase;
    font-weight: bold;
}
```

 **Goed:**
```css
.hidden {
    display: none;
}
```
```css
.no-border {
    border: none;
}
```
```css
.uppercase {
    text-transform: uppercase;
}
```

### Media queries
Zet niet alle rulesets voor mobiel in één media query. De volgorde van het document is belangrijker. 
Gebruik minimaal aantal breakpoints. Zorg dat de mogelijke breakpoints bovenaan in het document vast staan. 

### Gebruik van important
Probeer `!important` te vermijden!

1. Werkt het als ik `!important` toevoeg?
2. Welke stylesheet/ruleset overschrijft de definitie die je probeerd toe te voegen?
3. Kan je selector specifieker?

Zie:
- [Cascade and inheritance](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Cascade_and_inheritance)
- [Specificity]https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity
- [Which CSS entities participate in the cascadeSection](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade)


### (Optioneel) BEM
Formaat: `block-name__elem-name_mod-name_mod-val`  
Bem info: [[1]](https://en.bem.info/methodology/quick-start/)[[2]](http://getbem.com/introduction/)[[3]](http://getbem.com/naming/)

- Names are written in lowercase Latin letters.
- Words are separated by a hyphen (-).
- The block name defines the namespace for its elements and modifiers.
- The element name is separated from the block name by a double underscore (\_\_).
- The modifier name is separated from the block or element name by a single underscore (\_).
- The modifier value is separated from the modifier name by a single underscore (\_).
- For boolean modifiers, the value is not included in the name.

#### Block
✔ **Goed:**
```html
<ul class="main-menu"></ul>
```

#### Element
❌ **Fout:**
```html
<li class="item"></li>
<li class="main-menu-item"></li>
```

✔ **Goed:**
```html
<li class="main-menu__item"></li>
```

#### Modifiers
❌ **Fout:**
```html
<li class="main-menu__item active"></li>
<li class="main-menu__item-active"></li>
```

✔ **Goed:**
```html
<li class="main-menu__item_active"></li>
<li class="main-menu__item_color_blue"></li>
```
