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

### 3.4 Datatype `undefined`

Dit kan enkel de speciale waarde `undefined` bevatten. Deze staat voor een onbekende waarde (bv. een variabele waar nog geen waarde aan toegekend is)

### 3.5 Datatype `null`

Dit kan enkel de waarde `null` bevatten. Deze staat voor een lege object pointer.

> **(!)** Evalueert false in een boolean expressie.

### 3.5 Datatype `bigint`

Men gebruikt dit om gehele getallen voor te stellen die buiten het bereik van `number` vallen.

> **(!)** Gebruik de suffix `n` voor bigint literals
>
> ```JavaScript
> const aVeryBigNumber = 900719925474099199n;
> ```

### 3.6 Datatype `object`

Voorstelling van meer complexe datastructuren.
Later meer hier over.

### 3.7 Datatype `symbol`

Dit wordt gebruikt om unieke identifiers voor te stellen (bv. unieke namen,..).

## 4. Wrapper objects

Wrapper objects zijn objecten dat een primitief datatype 'omsluit'. Voorbeelden:

- `String`
- `Number`
- `BigInt`
- `Boolean`
- `Symbol`

> **(!)** Maak gebruik van `valueOf()` om de primitieve waarde voorgesteld door het wrapper object te achterhalen.

Het wrapper object geeft ons de mogelijkheid properties en methodes te gebruiken.

> **(!)** JavaScript past impliciete conversie toe, het primitieve getal wordt automatisch omgezet naar een wrapper object als je een methode van het wrapper object oproept.

### 4.1 [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)

Voorbeelden van methodes:

- Afronden tot x cijfers na de komma:
  - `toFixed(x)`
- String representatie, x is de radix, default 10
  - `toString(x)`

Voorbeelden van properties:

- Constante voor kleinste getal
  - `Number.MIN_VALUE`
- Constante voor grootste getal
  - `Number.MAX_VALUE`

### 4.2 [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)

- Object casten naar `Boolean`
  - `Boolean(x)`

Om te weten welke waarde er uit gaat komen, kijk naar puntje 3.2 in dit document.

### 4.3 [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)

- Object casten naar `String`
  - `String(x)`

### 4.4 [`BigInt`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)

- Object casten naar `BigInt`
  - `BigInt(x)` dit voegt eigenlijk gewoon 'n' toe aan een int

## 5. [`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) & [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) object

### 5.1 Het [`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) object

Het `Math` object is een built-in object dat properties en methodes bevat voor wiskunde constanten en functies. Het bevat enkel static properties en methods.

Enkele voorbeelden:

```JavaScript
console.log(Math.round(200.6)); //>>201
console.log(Math.max(200, 1000, 4)); //>>1000 (bv. in Array)
console.log(Math.min(200, 1000, 4)); //>>4
console.log(Math.random()); //getal tussen 0 en 1
```

### 5.2 Het [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) object

Houdt datums bij in milliseconden sinds 1/1/1970. Opgelet: kan enkel datums bijhouden 285.616 jaar ervoor en erna.

Creatie datum:

```JavaScript
const date = new Date(); //bevat de huidige datum/tijd
const date = new Date(1954,11,14,5,34,0,0); //jaar (4pos), maand (begint vanaf 0, dus waarde tussen 0 en 11), dag, uren, minuten, sec, msec)
```

Enkele methodes:

```JavaScript
const today = new Date();
console.log(today);
console.log(today.getFullYear());
console.log(today.getMonth()); //(start vanaf 0!!!)
console.log(today.getDate());
console.log(today.getHours());
console.log(today.getMinutes());
console.log(today.getSeconds());
console.log(today.getDay());
```

> **(!)** Zeer goed opletten: maanden liggen tussen 0 en 11. Dit betekent dat December de 11de maand is.

## 6. [Controlestructuren](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements)

- `if (..) {..}`

```JavaScript
if (scoops < 3) {
console.log('Ice cream is running low!');
}
```

- `if (..) {..} else {..}`

```JavaScript
if (scoops < 3) {
console.log('Ice cream is running low!');
} else if (scoops > 9) {
console.log('Eat faster, the ice cream is going to melt!');
}
```

- `switch (..) case ..`

```JavaScript
const d = new Date();
const theDay = d.getDay();
switch (theDay) {
  case 5:
  console.log('Finally Friday');
  break;
  case 6:
  console.log('Super Saturday');
  break;
  case 0:
  console.log('Sleepy Sunday');
  break;
  default:
  console.log("I'm really looking forward to this weekend!");
}
```

- `while (..) {..}`

```JavaScript
while (scoops > 0) {
  console.log('More icecream!');
  scoops--;
}
```

- `do {..} while (..)`

```JavaScript
do {
console.log('More icecream!');
scoops++;
} while (scoops < 10);
```

- `for (..) {..}`

```JavaScript
for (let berries = 5; berries > 0; berries--) {
  console.log('Eating a berry');
}
```

We kunnen herhalingen onderbreken met [`break`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/break) of [`continue`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/continue).

## 7. Operatoren

De meeste operatoren zijn gelijk aan bv. Java. Er is wel een belangrijke uitzondering. Er zijn 2 operatoren voor gelijkheid (`==` en `===`).

- `==`
  - er gebeurt impliciete type conversie, m.a.w. het type wordt niet gecontroleerd (m.a.w. 1 = '1')
- `===`
  - geen impliciete type conversie (m.a.w. 1 != '1')
  - dit is best practice

## 8. Functies

In JavaScript zijn er ook functies. Hiermee verkrijgen we efficiëntere code en elimineren we dubbele code.

Definitie:

```JavaScript
function functionname(par1,par2,...,parX) {
statements
};
```

Uitvoeren:

```JavaScript
functionname(arg1, arg2,….argx);
```

> **(!)** Merk op: er is hier geen datatype voor parameters en ook geen returntype!

- Gebruik van bestaande functies:
  - `alert("sometext")` alert box
  - `confirm("sometext")` confirm box
  - `prompt("sometext", "defaultvalue")` prompt box

## 8. Arrays

Een array is een geordende verzameling van elementen. De elementen **mogen van een verschillend** type zijn.

Arrays in JavaScript zijn **dynamisch**. Je moet dus geen startgrootte opgeven bij de declaratie.

Declaratie van een array:

```JavaScript
let pizzas = [];
//OF
let pizzas = new Array();
```

Waarden plaatsen in een Array:

```JavaScript
pizzas[0] = 'Margherita';
pizzas[1] = 'Mushroom';
pizzas[2] = 'Spinach & Rocket';
```
