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

//Enhanced for (kan voor objecten, voor arrays best bovenstaande loop gebruiken en kijken of iterator kleiner is dan arraysize (of forEach() gebruiken).)
for(let key in myAvatar) {
  console.log(`${key} : ${myAvatar[key]}`)
}
```

- ``

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

Je kan Arrays direct opvullen met waarden als volgt:

```JavaScript
let pizzas = ['Testwaarde1', 'Testwaarde2', 'Testwaarde3'];
```

Deze moeten niet allemaal hetzelfde zijn.

```JavaScript
let mixedArray = ['Testwaarde1', true, 1];
```

### 8.1 Array bewerken

Er zijn verschillende manieren om een Array te bewerken.

- `pop()` verwijdert het laatste element uit array
- `push('test')` voegt één of meerdere waarden toe aan het einde van de array
- `shift()` verwijdert de eerste waarde in array EN returnt deze
- `unshift()` voegt één of meerdere waarden toe aan het begin van het array

Je kan dingen verwijderen uit een array met het `delete` keyword.

```JavaScript
delete fruit[1];
```

### 8.2 Array methodes

- `concat()` voegt 2 arrays samen
- `reverse()` keert de volgorde van de array om
- `slice(start_index, upto_index)` returnt een nieuwe array als een stuk van de oorspronkelijke array (past oude array NIET aan)
- `splice(start_index, numberofItemsToRemove, nieuweWaarde1, ...)` voegt/verwijdert items toe/uit aan een array en returnt verwijderde items (past oude array aan)
- `sort()` sorteer de elementen in de array (past oude array aan)
- `indexOf(element)` returnt de index van het eerst voorkomende element dat gelijk is aan het doorgegeven element
- `lastIndexOf(element)` zelfde als indexOf(), maar begint achteraan
- `join()` converteert alle elementen van een array tot 1 lange string (met eventueel een concatenatieteken dat je tussen de haken kan declareren)

[Hier](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections#array_object) vind je meer informatie & methodes over Arrays.

### 8.3 Array destructuring

Je kan makkelijk meerdere waarden uit Arrays halen d.m.v. array destructuring.

Voorbeeld:

```JavaScript
//Variabele declaraties
//ophalen van eerste en tweede item uit een array
pizzas = ['Margherita', 'Mushroom', 'Spinach & Rocket', 'Chicken & Bacon'];
const [eerstePizza, tweedePizza] = pizzas;
console.log(eerstePizza); // Margherita
console.log(tweedePizza); // Mushroom
//ophalen van derde item uit een array
const [, , derdePizza] = pizzas;
console.log(derdePizza); //Spinach & Rocket
```

#### 8.3.1 Arrays copy (destructuring)

**Opgelet**: Als men een Array wilt kopiëren, dan kan dit niet zomaar met `a = b`. Dit is een hardlink. Alle aanpassingen die in b gebeuren, zullen ook in a gebeuren.

Om dit te vermijden kunnen we gebruik maken van array destructuring.

Voorbeeld:

```JavaScript
[...b] = a;
```

Dit zal een 'kopie' maken van array b en dit in a

## 9. Objecten en functies

Een object is een verzameling van properties, die het object beschrijven.

Een property heeft een naam en een waarde (key: value).

### 9.1 Objecten

Voorbeeld van een object:

```JavaScript
{
  key : value,
  key : value
}

// Een leeg object
const emptyObject = {};

//Object met waarden
const myAvatar = {
name: 'Bob',
points: 20,
gender: 'male',
hair: { color: 'black', cut: 'punk' }
};
```

#### 9.1.1 Properties uitlezen

Een waarde van een property uitlezen:

```JavaScript
//Arraynotatie
const name = myAvatar['name'];

//Puntnotatie
const points = myAvatar.points;

const haircolor = myAvatar.hair.color;
```

#### 9.1.2 Properties toevoegen

```JavaScript
//Arraynotatie
myAvatar['age'] = 18;

//Puntnotatie
myAvatar.age = 20;
```

Je kan ook onbestaande properties toevoegen. Dit doe je op dezelfde manier.

#### 9.1.3 Properties verwijderen

Dit doen we makkelijk met het `delete` keyword.

```JavaScript
//Arraynotatie
delete myAvatar['gender'];

//Puntnotatie
delete myAvatar.gender;
```

#### 9.1.4 Object destructuring

Dit is een krachtige manier om de waarden van properties vast te plakken.

```JavaScript
const { name, points, gender : sex} = myAvatar;

//Variabelen namen zijn nu name, points en sex.
```

### 9.1.5 Objecten overlopen

We kunnen objecten overlopen met een for loop. Voorbeeld:

```JavaScript
let result = '';
for (let key in myBicycle) {
  result += `${key} - ${myBicycle[key]}\n`;
}
alert(result);
```

We overlopen het object `myBicycle` en stoppen iedere iteratie de volgende key in de variabele `key`.

In het bovenstaande voorbeeld bouwen we een string op met de key en de waarde van de key.

### 9.1.6 Functies in objecten

Je kan perfect functies in objecten steken. Hieronder vind je een voorbeeld.

```JavaScript
const myBicycle = {
  speed: 30,
  gear: 1,
  frameMaterial: 'carbon fibre',
};

myBicycle.accelerate = function (percentage) {
  myBicycle.speed += (myBicycle.speed / 100) * percentage;
};

//Aanroepen van functie:
myBicycle.accelerate(25);
```

### 9.2 Functies

Functies zijn zoals in iedere andere taal blokken code die je kan aanroepen met parameters en eventueel waarden van kan terugkrijgen.

De functie declaratie:

- `function` keyword
- naam van de functie
- lijst van parameters
  - tussen ronde haakjes, gescheiden door komma's
- Javascript statements
  - de function body, tussen accolades

```JavaScript
function sayHi(name) {
return `Hi, my name is ${name}`;
}
```

**(!)** Je kan default waarden voor parameters voorzien. Dit door deze in de parameterlijst een waarde toe te kennen.

```JavaScript
function dyeHair(avatar, color = 'green') {
avatar.hair.color = color;
}
```

### 9.2.1 Return statements

Een return statement **stopt** verdere uitvoering van een function en retourneert een waarde naar de aanroeper van de functie.

> `return` kan overal geplaatst worden in de function body
>
> `return` kan meerdere malen in de function body voorkomen
>
> Indien het einde van de function body bereikt wordt zonder return statement, dan retourneert de functie `undefined`

Functie declaraties worden **gehoist**. Dit wil zeggen dat de declaratie als het ware naar boven wordt geplaatst.

### 9.2.2 Rest parameter

Via de rest parameter syntax kan je een onbeperkt aantal parameters voorstellen als een array. Je doet dit door de laatste parameter lijst te laten voorafgaan door `...`

```JavaScript
function f(a, b, ...otherArgs) {
  for (let value of otherArgs) {
    console.log(value);
  }
}
f(1, 2, 3, 'Four', 5);
```

Je kan hierbij ook gebruik maken van array destructuring.

```JavaScript
function f(a, b, ...[c, d, e, f]) {
  console.log(a);
  console.log(b);
  console.log(c);
  console.log(d);
  console.log(e);
  console.log(f);
}
f(1, 2, 3, 'Four', 5);
```

### 9.2.3 Arrow functions

Arrow functions zijn een **compactere syntax** om functie expressies te schrijven. Deze zijn altijd anoniem.

Algemene syntax:

```JavaScript
(par1, par2, …, parn) => {statements}
```

- Als er geen parameters zijn, gebruik `()`.
- Als er maar 1 parameter is, mag je `()` weglaten
- Als de code enkel de return van een expressie is, mag je `{}` en `return` weglaten.

```JavaScript
const function1 = (a, b, c) => {
  a = a + 1;
  return a + b + c;
};

const function2 = (a, b, c) => a + 1 + b + c;

const function3 = () => Math.random() * 20;
```

### 9.2.4 Functies toekennen aan variabele

Men kan makkelijk functies toekennen aan een variabele. Deze functies kunnen ook anoniem zijn.

```JavaScript
const dyeHair = function (avatar, color = 'green') {
avatar.hair.color = color;
}
dyeHair(myAvatar, 'yellow');
```

**(!)** Opgelet: Als je de variabele zonder haken aanroept, dan roep je de functie niet aan, maar refereer je naar de waarde van de variabele.

### 9.3 Closures

Closures zijn eigenlijk simpelweg functies die een innerfunctie retourneren. Die innerfunctie kan dan zo uitgevoerd worden.

Voorbeeld:

```JavaScript
function stringRepeater(nrOfTimes) {
  const repeater = function (msg) {
    let message = '';
    for (let i = 0; i < nrOfTimes; i++) message += msg;
    return message;
  };
  return repeater;
}

// Gebruik dit om je code te testen:
const stringDoubler = stringRepeater(2);
const stringTripler = stringRepeater(3);
console.log(stringDoubler('abc ')); // abc abc
console.log(stringTripler('def ')); // def def def
```

Het resultaat van stringRepeater() is dan de inner functie repeater met de toegewezen waarde nrOfTimes in de for loop.

### 9.4 Events

Als een object moet reageren op een bepaalde event, voorzie je een eventhandler of callback functie.
Wanneer het event getriggered wordt, zal de bijhorende event handler uitgevoerd worden.

- Gebruik de methode `getElementById('')` om een object op te halen die overeenkomt met de html tag met dat id

```JavaScript
const sayHiButton = document.getElementById('sayHi');
```

Een event heeft

- **een naam** - bv. click, change, load, mouseover, keyup, focus,...
- **een target** - het element waarop het event van toepassing is

Enkele voorbeelden:

- `onclick`, `onload`, `onmouseover`, `ondblclick`

```JavaScript
const init = function () {
  const h1 = document.getElementById('h1');
  h1.onmouseover = function () {
    this.innerHTML = this.innerHTML.slice(1, this.innerHTML.length);
  };
};

window.onload = init;
```

Meer info vind je [hier](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events).

### 9.5 Exceptions

Je kan exceptions gooien in geval van een ongebruikelijke fout

- `throw` gooit een exception object

```JavaScript
try {
  throw {
  name: 'SomethingWentWrongError',
  message: 'Something went wrong. You should fix it'
  };
} catch (e) {
  // handle the exception here
  console.log(`Error ${e.name}: ${e.message}`);
} finally {
  // this is executed even if an exception occurs
}
```

of kort:

```JavaScript
throw new Error('You must give the blog a title')
```

## 10. OOP in JavaScript

JavaScript is een object-gebaseerde taal gebaseerd op **prototypes**, in plaats van op klassen.

### 10.1 Klasse declaratie

De klasse declaratie maakt een nieuwe klasse aan gebruik makend van de prototype-gebaseerde overerving.

> **(!)** Klassen worden niet gehoist!

Standaard klasse layout:

```JavaScript
class ClassName {
  constructor (...) {...}

  method1 (...) {...}

  get someProperty() {...}
  set someProperty(value) {...}

  static staticMethod(...) {...}
}
```

Voorbeeld:

```JavaScript
class BlogEntry {
  constructor(body, date) {
  this.body = body;
  this.date = date;
  }
}
```

Om een nieuwe instantie te make van bovenstaande klasse, gebruikt men het keyword `new`.

```JavaScript
const aBlogEntry = new BlogEntry('This is the body', new Date(2008, 7, 16));
```

### 10.1.1 Constructor

Men stelt de constructor in met het keyword `constructor`. Hier kan men eventueel parameters aan meegeven.

We gebruiken `this` om properties te definiëren en eventueel te initialiseren.

```JavaScript
class Test {
  constructor(prop1, prop2) {
    this.prop1 = prop1;
    this.prop2 = prop2;
    this.prop3 = '';
  }
}
```

Indien in een klasse niet expliciet een constructor wordt gedefinieerd, dan heeft de klasse impliciet een parameterloze constructor.

> **(!)** Er is geen constructor overloading mogelijk. Je mag dus hoogstens 1 constructor definiëren.

Ook belangrijk om te weten: properties zijn publiek toegankelijk.

```JavaScript
Test.prop1 = 'I love bananas';
console.log(Test.prop1);
```

Dit is eigenlijk _not done_. We willen gebruik maken van private properties met getters & setters.

### 10.1.2 Getters & setters (& private properties)

De naam van een property die niet publiek zou mogen gebruikt worden laten we voorafgaan door een **underscore** (the way it should be done!).

```JavaScript
class BlogEntry {
  constructor(body, date) {
    this._body = body;
    this._date = date;
  }
}
```

We voorzien in de klasse nu een publieke interface (publieke methodes, getters & setters die gebruik maken van de private properties).

- **getter**

We gebruiken het keyword `get` gevolgd door de naam van de property.

```JavaScript
class BlogEntry {
  constructor(body, date) {
    this._body = body;
    this._date = date;
  }

  get body() { return this._body; }
  get date() { return this._date; }
}

//Oproepen van getters:
const aBlogEntry = new BlogEntry('...');
console.log(`body: ${aBlogEntry.body}`);
console.log(`date: ${aBlogEntry.date}`);
```

Merk op: de get syntax associeert een functie met een property maar je roept die functie niet expliciet op. De get functie wordt uitgevoerd als de waarde van de property gelezen moet worden.

- **setters**

We gebruiken het keyword `set` gevolgd door de naam van de property. Je kan exact 1 parameter gebruiken (de waarde die we wensen toe te kennen aan de property).

```JavaScript
class BlogEntry {
  constructor(body, date) {
    this._body = body;
    this._date = date;
  }

  get body() { return this._body; }
  set body(value) {
    this._body = value;
  }
  get date() { return this._date; }
}

//Oproepen van getters:
const aBlogEntry = new BlogEntry('...');
console.log(`body: ${aBlogEntry.body}`);
console.log(`date: ${aBlogEntry.date}`);
```

### 10.1.3 Methods

Methods zijn hetzelfde als functies, maar dan in een klasse.

```JavaScript
class BlogEntry {
  constructor(body, date) {
    this._body = body;
    this._date = date;
  }

  get body() { return this._body; }
  set body(value) {
    this._body = value;
  }
  get date() { return this._date; }

  resetBody() {
    this._body = '';
  }
}
```

Men kan deze methode dan makkelijk aanroepen met `BlogEntry.resetBody();`

Je kan ook static methods maken. Dit doe je op exact dezelfde manier als gewone methods, maar je plaatst het keyword `static` voor de methodenaam.

Voorbeeld: `static createDummy() { return new this('Nothing much to say'); }`

### 10.2 Prototypes

In JavaScript is alles een object, er bestaan geen klassen zoals we die kennen uit Java. Via prototype objecten kunnen objecten toestand en gedrag delen.

- een object heeft zijn eigen properties en methodes
- een object heeft een property `__proto__`
- `__proto__` is het prototype object via dewelke het object gedrag en toestand erft

> Het prototype object is ook maar een object. Dit wil zeggen dat deze op zijn beurt ook een prototype object heeft. Zo ontstaat er een ketting van prototype objecten: **prototype chain**.

Men kan dan een property toevoegen aan het prototype van een object. Kortweg is dit een soort 'globale' variabele voor alle objecten van dit type. Een voorbeeld:

```JavaScript
const myBlogEntry = new BlogEntry('Prototypes rock!');
const anotherEntry = new BlogEntry('JavaScript rules!');
BlogEntry.prototype.language = 'EN';
console.log(myBlogEntry.language); // EN
console.log(anotherEntry.language); // EN
```

Als je achteraf de property nog gaat bijwerken, maar niet van de property, dan is dit van het object zelf. Voorbeeld:

```JavaScript
const myBlogEntry = new BlogEntry('Prototypes rock!');
const anotherEntry = new BlogEntry('JavaScript rules!');
BlogEntry.prototype.language = 'EN';

console.log(myBlogEntry.language); // EN
console.log(anotherEntry.language); // EN
myBlogEntry.language = 'NL';
console.log(myBlogEntry.language); // NL
console.log(anotherEntry.language); // EN
```

Dit kan ook perfect met bv. functions.

```JavaScript
const myBlogEntry = new BlogEntry('Prototypes rock!');
const anotherEntry = new BlogEntry('JavaScript rules!');
BlogEntry.prototype.language = 'EN';
BlogEntry.prototype.contains = function(searchText) {
  return this.body.toUpperCase().indexOf(searchText.toUpperCase()) !== -1;
};
```

## 11. Functioneel programmeren

> Functional programming is the process of
> building software by composing pure functions,
> avoiding shared state, mutable data, and side effects. Functional programming is declarative
> rather than imperative, and application state
> flows through pure functions.

- **Pure functions**

Een pure functie is een voorspelbare functie.

- Als je de functie aanroept krijg je met dezelfde input, steeds dezelfde output
- Geen side-effects (DOM manipulatie, externe variabelen wijzigen,...)

- **Shared state**

Een shared state is elke variabele of object die bestaat in een gedeelde scope of die wordt doorgegeven naar een andere scope.

```JavaScript
// Een gedeelde variabele creëren
let gedeeldeVariabele = 0;
function verhogen(){
  gedeeldeVariabele += 1;
}
function verdubbelen(){
  gedeeldeVariabele *= 2;
}
verhogen();
console.log(gedeeldeVariabele);
verdubbelen();
console.log(gedeeldeVariabele);
```

- **Mutable vs Immutable**

```JavaScript
// Een array maken (muteerbaar)
const hobbies = [
‘programmeren’,
‘gamen’,
‘voetbal’
];
const omgekeerdeHobbies =
hobbies.reverse();
console.log(omgekeerdeHobbies);
//[‘voetbal’, ‘gamen’, ‘programmeren’]
console.log(hobbies);
//[‘voetbal’, ‘gamen’, ‘programmeren’]

//-------------------------------------

// Een string maken (niet-muteerbaar)
const origineel = "Ik ben niet muteerbaar";
const gewijzigd = origineel.replace("Ik ben niet muteerbaar", "Ik ben gewijzigd");

console.log(gewijzigd);
// "Ik ben gewijzigd"
console.log(origineel);
// "Ik ben niet muteerbaar"
```

- **Side-effects**

Een side effect is iedere verandering aan de toestand van een applicatie die zichtbaar is buiten de opgeroepen functie (behalve de return waarde).

- **Declaratief vs Imperatief**

- Imperatief

Focust op _hoe_ een programma functioneert. Bestaat uit een beschrijving van de verschillende uit te voeren stappen om een resultaat te bereiken: **flow control**.

- Declaratief

Focust op _wat_ een programma moet bekomen, zonder te specifiëren hoe dit moet bekomen worden (meer black box).

Declaratief maakt gebruik van bestaande functies om de complexheid te verminderen.

### 11.1 Arrays

Korte herhaling i.v.m. lussen:

```JavaScript
// De klassieke manier
for (let i = 0; i < fruit.length; i++) {
  console.log(fruit[i]);
}
// Nog een manier met behulp van for-of
for(let element of fruit){
  console.log(element);
}
```

### 11.2 Callback functies

Er zijn een aantal geavanceerde methodes voor arrays. Deze werken met het concept van een callback functie. Een callback functie is een functie die wordt uitgevoerd **NADAT** een andere functie klaar is.

Denk maar aan een event listener.

```JavaScript
button.addEventListener('click', callBackFunction);
```

De functie `callBackFunction` zal pas NA het click-event worden afgehandeld.

Je kan dit ook manueel doen door de functie mee te geven aan de eerste functie. Voorbeeld:

```JavaScript
function doHomework(subject, callback) {
  console.log(`Starting my ${subject} homework.`);
  callback();
}
function alertFinished(){
  console.log('Finished my homework');
}
doHomework('math', alertFinished);
```

### 11.3 Map - Filter - Reduce

[`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map), [`Filter`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) en [`Reduce`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) zijn geavanceerde methodes van de Array die de functionele programmeerstijl onderschrijven aan de hand van een callback functie.

We moeten dus aan deze methodes een callback functie meegeven. Normaliter doen we dit met de array notatie, maar dit is niet verplicht.

De callback functie wordt opgeroepen voor **ieder** item in de array. Bij iedere iteratie krijgt de functie automatisch een aantal argumenten mee:

- `Value` - de huidige waarde tijdens de iteratie
- `Index` - de huidige index (teller) van de iteratie
- `Array` - een kopie van de hele array

> **(!)** Al deze methodes geven een nieuwe array terug, ze passen de oude array **NIET** aan.

We hebben dus 3 manieren waarop we dit kunnen noteren.

1. Aparte (niet anonieme) functie

```JavaScript
arr.map(callbackFunctie);

function callbackFunctie(value, index, array) {
  return ...;
}
```

2. Inline versie met anonieme functie

```JavaScript
arr.map(function(value, index, array) {
  return ...;
});
```

3. Arrow notatie **(aanbevolen)**

```JavaScript
arr.map((value, index, array) => {...})
```

### 11.3.1 Filter

Stel: je hebt een array en wilt bepaalde items er uit filteren. Dan gebruik je het best `filter`. Het resultaat is een **nieuwe** array met enkel de items die aan de filter voldoen.

```JavaScript
//Dit zal alle waarden kleiner dan 6 returnen in een nieuwe array.
let filteredArray = arr.filter((waarde) => waarde < 6);
```

### 11.3.2 Map

Je gebruikt `Map` wanneer je een reeks items wilt transformeren. Het resultaat is een nieuwe array van exact dezelfde lengte die de gemanipuleerde items bevat.

```JavaScript
// arr = [5, 10]
let filteredArr = arr.filter((waarde) => waarde * 10);
// filteredArr = [50, 100]
```

### 11.3.3 Reduce

Je gebruikt `Reduce` wanneer je van een reeks items een nieuwe waarde wilt berekenen. Het resultaat kan van alles zijn (een andere array, nieuw object, booleanse waarde,...).

```JavaScript
const aantalGeslaagden = function(acc, element) {
  return (element >= 10) ? acc + 1 : acc;
}
const passed = [10, 8, 12, 15, 4].reduce(aantalGeslaagden, 0);
//passed = 3
```

> **(!)** Vergeet zeker de startwaarde niet in te stellen (de 0 op het einde).

### 11.4 Geavanceerde methodes

- **`forEach()`**

Dit is een generische functie die over een array itereert en een callback functie aanroept tijdens elke iteratie.

```JavaScript
fruit.forEach((element) => console.log(element));
```

Zoals de bovenstaande functies, heeft de `forEach` functie ook een `value`, `index` en `array` waarde.

```JavaScript
fruit.forEach((item, index, array) => {
  console.log(`${item} is at index ${index} in ${array}`);
});
```

- **`find`** & **`findIndex`**

Retourneert (de index van) het eerste element waarvoor de callback voorwaarde true retourneert (dus hetzelfde als `indexOf`, maar hier kan je er een voorwaarde bijstoppen).

```JavaScript
let result = original.find(p => p.firstname === 'Piet');
```

> **(!)** Als er niets gevonden is, retourneert `findIndex` -1 en `find` _undefined_.

### Tips & tricks

- Tekstveld uitlezen: `document.getElementById('test').value`
- Element src bewerken: `document.getElementById('test').src = 'img/test.png'`
- String individuele character: `string.charAt(0)`
- Om iets in een string te zoeken, gebruiken we `str.includes()`
- Willekeurig getal genereren: `Math.floor(Math.random() * 10) + 1` (tussen 1 en 10)
- Enhanced for bij Arrays:

```JavaScript
for(let element of fruit){
  console.log(element);
}
```
