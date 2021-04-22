# Web Development II (JavaScript) examensamenvatting

Door Brooklyn Dewolf (HoGent, Bach. Toegepaste Informatica)

Alle onderstaande info en voorbeelden komen uit de slides van Web Development II.

## 1. Basis en inleiding (JavaScript in HTML)

### 1.1 Implementatie in HTML

Je kan JavaScript op 2 manieren in jouw website integreren.

1. Rechtstreeks in het HTML document met de `<script>` tag.

```HTML
<script>
document.getElementById("demo").innerHTML = "Hello JavaScript!";
</script>
```

2. In een apart JavaScript bestand (dan moet er wel een link worden gelegd vanuit het HTML bestand).

```HTML
<script src="/js/hello.js"></script>
```

> **(!)** We zetten de script tag vanonder in het `<body>` element zodat alle HTML elementen eerst worden ingeladen voor dat het JavaScript bestand uitgevoerd wordt.

### 1.4 Commentaar & console output

In JavaScript kunnen we dingen in commentaar zetten zoals bij andere talen. Dit doen we als volgt:

- `//` single line comment
- `/* */` multi line comment

We kunnen ook dingen naar de console loggen.
Dit doen we met `console.log('Hello!');`

Ook popups zijn mogelijk. Dit kan met `alert('Hello');`.

### 1.3 JS strict mode

De komst van ES5 in 2009 introduceerde 'breaking changes' in de JavaScript taal. Dit had onderstaande gevolgen:

- niet alle oude code kon uitgevoerd worden met de introductie van de nieuwe features
- daarom werden de nieuwe 'breaking' changes standaard uitgeschakeld

We kunnen de nieuwe features inschakelen door `'use strict';` helemaal vanboven in het JavaScript bestand te plaatsen.

> **(!)** Maak je gebruik van classes en modules, dan staat de werken we automatisch in strict mode.

## 2. Variabelen

JavaScript gebruikt zoals vele andere talen variabelen om data bij te houden. In tegenstelling tot bij Java, moeten we **geen** datatype meegeven bij de declaratie.

We hebben 2 types:

- `let`

Dit gebruiken we om een variabele te declareren die we achteraf pas gaan initialiseren of aanpassen.

```JavaScript
let username;
username = 'Anne-Marie';
```

- `const`

Dit is een variabele die je moet initialiseren bij declaratie en die nadien niet meer van waarde kunnen veranderen.

```JavaScript
const username = 'Anne-Marie';
```

> **(!)** Het is good practice om zoveel mogelijk `const` te gebruiken. Beperk het gebruik van `let` tot echte variabelen die van waarde moeten kunnen veranderen.

## 3. Datatypes

JavaScript kent 8 basis datatypes.

- `number` - getallen
- `bigint` - hele grote gehele getallen
- `string` - tekst bestaande uit 0 of meerdere karakters
- `boolean` - logische waarden: true/false
- `null` - ongekende waarde
- `undefined` - voor niet toegekende waarden
- `object` - voor meer complexe datastructuren
- `symbol` - voor unieke identifiers

> **(!)** JavaScript is een _dynamically typed_ language. Dit betekent dus dat het type van een variabele wordt bepaald _at run-time_.
>
> Het type van een variabele kan wijzigen naar mate dat het uitvoeren van de code vordert.
>
> ```JavaScript
> let dynamisch;
> dynamisch = 'Nu is het een string';
> dynamisch = 5; //nu is het een number
> ```

### 3.1 Datatype `number`

- gehele en floating point getallen
- integer literals
  - decimaal: 3, 10,...
  - prefix `0x` voor hexadecimaal
  - prefix `0o` voor octaal
  - prefix `0b` voor binair
- basis operatoren
  - `+`, `-`, `*`, `/`, `%`

> **(!)** Je hebt precisie tot op 17 cijfers na de komma.

- speciale waarden
  - `NaN` - (Not a Number)
    - om iets dat niet kan voorgesteld worden als getal te beduiden
    - je kan `isNan()` gebruiken om een te zien of een variabele de `NaN` waarde heeft. Dit is een boolse functie.
  - `Infinity` - oneindig getal
    - je kan `isFinite()` gebruiken om te kijken of een variabele oneindig groot is. Dit is een boolse functie.

Enkele voorbeelden van `NaN` en `Infinity`:

```JavaScript
const fail = 10 / "zero";
console.log(fail); // >> NaN (Not a Number)
console.log(isNaN(fail)); //>>true
console.log(isNaN(10)); //>>false
console.log(isNaN('10')); //>>false
console.log(isNaN('blabla')); //>>true
console.log(isNaN(true)); //>>false
console.log(1.7976931348623157e+308 * 1000); //>> Infinity
console.log(1.7976931348623157e+308 * -1000); //>>- Infinity
console.log(10 / 0); //>>Infinity
console.log(isFinite(123)); //>>true
```

Je kan ook conversies uitvoeren op `string` en `number` objecten.

- `parseInt(aString)` - converteert string naar geheel getal
- `parseFloat(aString)` - converteert string naar floating point

Beide doorlopen de string tot ze het eerste ongeldige karakter tegenkomen. Hieronder vind je enkele voorbeelden:

```JavaScript
console.log(parseInt('1234numbers')); //>>1234
console.log(parseInt('$1234')); //>>NaN
console.log(parseInt('22.5')); //>>22
console.log(parseFloat('1234numbers')); //>>1234
console.log(parseFloat('$12.34')); //>>NaN
console.log(parseFloat('22.34.15')); //>>22.34
console.log(parseFloat('22.5')); //>>22.5
```

### 3.2 Datatype `boolean`

Een `boolean` kan een logische waarde bevatten (`true` of `false`). Opgelet: case sensitive!

Alle waarden in JavaScript hebben een bools equivalent, dit wordt gebruikt bij impliciete conversies:
| datatype | converteert naar `true` | converteert naar `false` |
|-----------|-------------------------|--------------------------|
| boolean | true | false |
| string | niet lege string | "" (lege string) |
| number | een niet 0 getal | 0, NaN |
| object | elk object | null |
| undefined | | undefined |

### 3.3 Datatype `string`

Bevat een sequentie van 0 of meer Unicode karakters.

Bij het gebruik van de `+` operator gebeurt er een concatenatie van 2 strings.

```JavaScript
const c = 'first text' + 'second text'; //Immutable
console.log(c); //>> "first textsecond text"
```

Je kan ook een conversie doen naar een string:

- `toString(var)` - een datatype omzetten naar een string

Voorbeeld:

```JavaScript
const getal = 12;
const b = true;
console.log(getal.toString()); //>> 12;
console.log(b.toString()); //>> true;
console.log(null.toString()); //geeft een exception. >>Uncaught
TypeError: Cannot read property 'toString' of null
```

Om makkelijk variabelen in strings te gebruiken, maken we gebruik van **template literals**:

- worden omsloten door backticks \``
- multiline strings zijn mogelijk
- expressies in de string evalueren

Een voorbeeld:

```JavaScript
const a = 5;
const b = 10;
console.log(`Fifteen is ${a + b} and
not ${2 * a + b} and not ${b}.`);
// "Fifteen is 15 and
// not 20."
```
