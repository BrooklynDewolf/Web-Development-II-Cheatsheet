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

> Opgelet: Door `delete` te gebruiken zal er `undefined` in de lijst te komen staan. Om dit te voorkomen gebruiken we `arr.splice()`

```JavaScript
fruit.splice(1, 1);
// Dit zal de waarde op index 1 verwijderen.
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

Nog een voorbeeld:

```JavaScript
imgElem.onclick = () => {
        this.verwijderZoekterm(value);
};
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

### 10.3 `toString()` methode

In de klassedeclaratie van een JavaScript class object kan je ook een `toString()` methode toevoegen. Deze wordt automatisch aangeroepen wanneer men bv. met `console.log(obj);` een object logt.

```JavaScript
toString() {
    return `Rechthoek met breedte= ${this._width} en hoogte = ${this._height}`;
  }
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

### 11.3.2 Map (function)

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

Voorbeeld met arrow function:

```JavaScript
console.log(inventors.reduce((acc, value, index, array) => acc + (value.passed - value.year), 0));

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

- **`find()`** & **`findIndex()`**

Retourneert (de index van) het eerste element waarvoor de callback voorwaarde true retourneert (dus hetzelfde als `indexOf`, maar hier kan je er een voorwaarde bijstoppen).

```JavaScript
let result = original.find(p => p.firstname === 'Piet');
```

> **(!)** Als er niets gevonden is, retourneert `findIndex()` -1 en `find()` _undefined_.

- **`sort()`**

We gebruiken `sort()` om een array te sorteren. Tussen de haken kunnen we een comparator meegeven. Indien je geen comparator voorziet, worden de elementen van de array omgezet naar strings en wordt er 'alfabetisch' gesorteerd.

> **(!)** De array wordt **in-place** gesorteerd, dit wil zeggen dat de sort function de gesorteerde array retourneert, dit is dus **GEEN** kopie van de originele array.

```JavaScript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort();
```

Voorbeeld van compare methode:

```JavaScript
function compare(a, b) {
  if (a > b) return 1; // een positief getal betekent dat a groter is dan b
  if (a == b) return 0;
  if (a < b) return -1; // een negatief getal betekent dat a kleiner is dan b
}
```

Een korter geschreven sort methode:

```JavaScript
fruit.sort((a, b) => a.length - b.length);
```

Er bestaan nog veel meer handige array methodes (zie [MDN website](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)).

### 11.4 Maps (storage)

Het `Map` object bevat key-value pairs. Het onthoudt de originele volgorde waarop de keys in de map zijn gestoken.

Om een nieuwe `Map` te maken, gebruiken we de constructor van `Map`:

```JavaScript
const population = new Map();
```

- **`set()`**

Om key-value pairs toe te voegen in de map gebruiken we de `set()` functie.

```JavaScript
population.set('Belgium', 11589623);
population.set('Burkina Faso', 3273);
```

De `set()` functie retourneert de aangepaste map, dit maakt method chaining mogelijk.

```JavaScript
population
  .set('Belgium', 11589623)
  .set('Burkina Faso', 20903273);
```

- **`get()`**

De `get(key)` functie geeft de value weer dat bij de key hoort. Als de key niet gevonden is, wordt `undefined` geretourneerd.

```JavaScript
console.log(population.get('Belgium')); //11589623
```

- **`has()`**

De `has(key)` functie retourneert een boolean die aangeeft of een try met de opgegeven key aanwezig is in de Map.

```JavaScript
if (population.has(country))
  alert(`${population.get(country)} people live in ${country}`);
else
  alert(`We have no data for ${country}`);
```

- **`delete()`**

Via de boolse methode `delete(key)` kan je een entry met opgegeven key verwijderen uit een Map.

```JavaScript
if (population.delete(country))
  alert(`The entry for ${country} was deleted`);
else
  alert(` Couldn't not delete ${country}...`);
```

- **`clear()`**

Gebruik `clear()` om een map in 1 stap te ledigen.

```JavaScript
population.clear();
```

- **`keys()`**

De `keys()` methode retourneert een itereerbaar object met alle keys. Je kan deze overlopen met `for .. of`.

```JavaScript
message = 'Keys in our map:\n';
for (const key of population.keys()) {
  message += `${key}\n`;
}
alert(message);
```

- **`values()`**

De `values()` methode retourneert een itereerbaar object met alle values. Je kan deze overlopen met `for .. of`.

- **`entries()`**

De `entries()` methode retourneert een itereerbaar object met alle entries. Iedere entry zit in een array van lengte 2.

```JavaScript
message = 'Entries in our map:\n';
for (const entry of population.entries()) {
  message += `${entry[0]} has ${entry[1]} people.\n`;
}
alert(message);
```

> **(!)** TIP: Maak gebruik van array destructuring:
>
> ```JavaScript
> for (const [key, value] of population.entries()) {
>   message += `${key} has ${value} people.\n`;
> }
> ```

- **`forEach()`**

Op Map is ook de `forEach(callback)` gedefineerd. Nu weliswaar met 3 andere argumenten: `value`, `key`, `Map` (exacte volgorde).

> Via de `size` property kan je weten hoeveel key-value pairs een map bevat.
>
> ```JavaScript
> alert(`We have data for ${population.size} countries.`);
> ```

### 11.4.1 Map constructor revisited

Je kan een array argument gebruiken om een map te creëren met een aantal entries. In deze array stop je key-value pairs in de vorm `[key, value]`.

```JavaScript
population = new Map([
  ['Belgium', 11589623],
  ['Burkina Faso', 20903275],
  ['Iceland', 341243],
]);
```

### 11.4.2 Objecten als keys

```JavaScript
const bel = {
  name: 'Belgium',
  region: 'Europe'
};

population.set(bel, 11589623);
alert(`${population.get(col)} live in
${col.name}`);
```

### 11.5 Sets

Het `Set` object onthoudt **unieke** waarden (er zijn dus geen duplicate waarden).

```JavaScript
let viewers = new Set();

//of direct met initiële waarden
let viewers = new Set(["bill.gates@microsoft.com", "elon.musk@tesla.com", "michael.scott@dundermifflin.com"]);
```

- **`add()`**

Met de `add(value)` methode kan je dingen toevoegen aan een `Set`, indien de value nog niet aanwezig is. De methode returned de al dan niet gewijzigde set.

Je kan de `add()` methode ook chainen.

```JavaScript
viewers
.add('michael.scott@dundermifflin.com')
.add('bill.gates@microsoft.com');
```

- **`has()`**

De `has(value)` methode retourneert een boolean die aangeeft of de opgegeven value aanwezig is in de `Set`. Zoals bij de `Map` wordt er hier ook gebruik gemaakt van `===`.

> Met de `size` property kunnen we het aantal values opvragen in de `Set`.

- **`delete()`**

Via de boolse methode `delete(value)` kan je een value verwijderen uit een `Set`.

We kunnen `clear()` gebruiken om de hele `Set` direct te ledigen.

- **`values()`** en **`entries()`**

  - `values()` retourneert een itereerbaar object met alle values
  - `entries()` retourneert een itereerbaar object met alle [value, value] pairs (enkel voor compatibiliteit met Map)

- **`forEach()`**

Een `Set` heeft ook een de `forEach(callback)` gedefinieerd.

De callback heeft 3 argumenten: `currentValue`, `currentKey` en `set`.
Omdat `Set` geen keys heeft, is `currentKey` gelijk aan `currentValue`.

```JavaScript
let message = 'All strings in the set:\n';
viewers.forEach((value) => message += typeof value === 'string' ? `${value}\n` : '');
alert(message);
```

### 11.6 Rest & spread syntax

### 11.6.1 Spread syntax

Via de spread syntax kunnen we iterable 'uitklappen' in afzonderlijke elementen. Deze elementen kunnen dan gebruikt worden

- als argumenten bij functie aanroepen
- als elementen van een array bij de array literal notation

Voorbeeld:

```JavaScript
const numbers = [20, 30, 40, 50];
//Op plaatsen in je script waar je 20, 30, 40, 50 wil gebruiken kan je ...numbers zetten.

//Bv. in een functieaanroep Math.max(1, 20, 30, 40, 50, 8); wordt =>
Math.max(1, ...numbers, 8);

//Bv. in een array literal const numbers2 = [-1, 5, 11, 20, 30,40, 50]; wordt =>
const numbers2 = [-1, 5, 11, ...numbers];
```

Je kan de spread syntax gebruiken om bepaalde dingen 'om te vormen'. Bijvoorbeeld:

- `string` -> karakters
- `map` -> [key, value] pairs
- `map.keys()` -> keys
- `map.values()` -> values
- `set` -> values
- `set.values()` -> values
- `array` -> elementen

Voorbeeld:

```JavaScript
const aSet = new Set(["tom.antjon@hogent.be", "
stefaan.decock@hogent.be"]);
console.log([1, 2, ...aSet, 3, 4]);

//OUTPUT: (6) [1, 2, "tom.antjon@hogent.be", "stefaan.decock@hogent.be", 3, 4]

const aMap = new Map([
['Belgium', 11589623],
['Burkina Faso', 20903275],
['Iceland', 341243],
]);

const numbers = [-1, 5, 11, 3];
console.log(Math.max(...numbers)); // 11
console.log(Math.max(1, 10, ...numbers, 20, 2)); //20
console.log(Math.max(...aMap.values())); //20903275
```

Je kan de spread operator ook gebruiken om arrays samen te voegen:

```JavaScript
const arr1 = ['Jan', 'Piet'];
const arr2 = ['Joris', 'Korneel'];
// maak een shallow copy die de inhoud van beide arrays bevat:
const arr12 = [...arr1, ...arr2];
console.log(arr12); // ["Jan", "Piet", "Joris", "Korneel"]
// voeg aan arr1 de elementen van arr2 toe
arr1.push(...arr2);
console.log(arr1); // ["Jan", "Piet", "Joris", "Korneel"]
```

Door verschillend functies samen te voegen kan men krachtige dingen doen. Enkele voorbeelden:

```JavaScript
//Map aanpassen zodat enkel landen met meer dan 5000000 inwoners overblijven
console.log(`Original map:`);
console.log(population);
population = new Map([...population].filter(
([country, population]) => population > 5000000));
console.log(`Map without big countries:`);
console.log(population)
```

### 11.6.2 Rest parameter

Via de rest parameter syntax kunnen we een onbepaald aantal argumenten aanleveren aan de parameter van een functie. **Dit moet de laatste parameter van een functie zijn**.

```JavaScript
function showName(lastname, ...firstnames) {
  console.log(`De parameter firstnames bevat ${firstnames}`);
  const i = firstnames.reduce((initials, value) => initials + value[0], '');
    return `${i} ${lastname}`;
  }
console.log(showName('Rowling', 'Joanne', 'Kathleen')); //JK Rowling
console.log(showName('Rubens', 'Pieter', 'Paul')); //PP Rubens
```

Het `rest` pattern laat ook toe het resterende deel van een array vast te nemen in een een variabele tijdens array destructuring.

```JavaScript
const [a, ...b] = ['Jan', 'Piet', 'Korneel', 'Steven', 'Maarten'];
console.log(a); //Jan
console.log(b); //['Piet', 'Korneel', 'Steven', 'Maarten']
```

> **(!)** Je kan de rest operator enkel bij de laatste in de rij van variabelen zetten.

### 12. Webstorage

Er zijn verschillende soorten webstorage, denk maar aan:

- Cookies
- Session Storage
- Local Storage
- IndexedDB (niet behandeld in de cursus)

### 12.1 Cookies

Cookies worden meestal ingesteld door een webserver. Vervolgens voegt de browser ze automatisch toe aan (bijna) iedere request op hetzelfde domein.

Cookies zijn een ingebouwde manier om kleine tekstbestanden heen en weer te sturen tussen de browser en de server. Servers kunnen gebruik maken van de inhoud van deze cookies om informatie over de gebruiker bij te houden over verschillende webpagina's heen.

Cookies blijven bestaan, ook als je de tab of browser sluit. De cookie kan manueel verwijderd worden, of wordt automatisch verwijderd indien de vervaldatum bereikt is.

### 12.1.1 Cookie-structuur

Een cookie is gevormd door `key-value pairs` gescheiden door `;`.

Voorbeeld:

```JSON
"user=John; path=/; expires=Tue, 19 Jan 2038 03:14:07 GMT"
```

Cookies hebben verschillende opties, veel daarvan zijn belangrijk en moeten worden ingesteld:

- `path`
- `domain`
- `expires`, `max-age`
- `secure`
- `httpOnly`

### 12.1.2 Cookies toevoegen en verwijderen

Om cookies toe te voegen, kunnen we naar `document.cookie` schrijven, maar het is geen data eigenschap, het is een accessor (getter/setter). Een schrijfoperatie naar `document.cookie` werkt alleen de cookies bij die erin worden genoemd, maar muteert geen andere cookies.

**Cookie instellen**

```JavaScript
document.cookie = 'taal=NL';
```

**Cookie verwijderen**

Om een cookie te verwijderen stellen we de `max-age` in op 1 seconde in het verleden.

```JavaScript
document.cookie = 'taal=;max-age=-1'
```

### 12.1.3 Cookies encoderen

Technisch gezien kunnen key en value alle karakters hebben, om de geldige opmaak te behouden (spaties) moeten ze worden escaped met behulp van de ingebouwde `encodeURIComponent` functie.

```JavaScript
const name = "my name"; // let op de spatie
const value = "John Smith"
const encodedName = encodeURIComponent(name);
const encodedValue = encodeURIComponent(value);
// encodes the cookie as my%20name=John%20Smith
document.cookie = encodedName + '=' + encodedValue;
alert(document.cookie); // ...; my%20name=John%20Smith
```

### 12.2 Webstorage

De webstorage objecten `localStorage` en `sessionStorage` maken het mogelijk om key/value pairs op te slaan in de browser.

Interessant is dat de data een pagina refresh overleeft (`sessionStorage`) en zelfs een volledige herstart van de browser (`localStorage`).

**Verschillen met cookies**

- Data wordt niet bij iedere request verstuurd.
- Kan meer data stockeren, maar is geen databank zoals SQL.
- De server kan de data niet manipuleren, alles blijft op de client.
- Per domein, de ene website kan de data van een andere dus niet muteren.
- Data is toegankelijk voor de gebruiker, bij cookies kan het zijn dat de server de cookie zet en is dus niet leesbaar door `httpOnly`.

**Verschillen tussen `localStorage` en `sessionStorage`**

- `localStorage`
  - Beschikbaarheid van data over meerdere tabbladen/vensters van hetzelfde domein
  - Data blijft beschikbaar als het venster, tabblad of browser sluit
- `sessionStorage`
  - Beschikbaarheid per tabblad/venster, wordt niet gedeeld met een ander venster of tabblad
  - Data is verdwenen na het sluiten van venster of tabblad.

**Nadelen van webstorage**

- Er kunnen enkel strings opgeslagen worden
- De inhoud kan door de gebruiker bekeken, gewijzigd en verwijderd worden.
- Per domein.

### 12.2.1 Webstorage bewerken

Voor zowel `localStorage` als `sessionStorage` gebruikt men de `Storage` interface.

- **Data opslaan**

```JavaScript
localStorage.setItem('test', 1);
```

> Let op: Beide zijn uiteindelijk van het type `string`

- **Data ophalen**

```JavaScript
console.log(localStorage.getItem('test')); // 1
```

- **Data verwijderen**

```JavaScript
localStorage.removeItem('test');
```

- **Alle data verwijderen**

```JavaScript
localStorage.clear();
```

- **Alle key-value pairs doorlopen (als object)**

```JavaScript
for(let key in localStorage) {
  alert(key); // shows getItem, setItem and other built-in stuff
}
```

> Opgelet: hier worden ook de built-in fields teruggegeven

Als object itereren zonder built in fields:

```JavaScript
for(let key in localStorage) {
  if (!localStorage.hasOwnProperty(key)) {
    continue; // skip keys like "setItem", "getItem" etc
   }
  alert(`${key}: ${localStorage.getItem(key)}');
}
```

- **Alle key-value pairs overlopen (als object, zonder built in fields)**

Hiervoor gebruiken we `Object.keys(localStorage)`.

```JavaScript
let keys = Object.keys(localStorage);
for(let key of keys) {
  alert(`${key}: ${localStorage.getItem(key)}');
}
```

Via de `Object.entries` methode, key-value pairs doorlopen

```JavaScript
for (let [key, value] of Object.entries(localStorage)) {
  console.log(`${key}: ${value}');
}
```

### 12.3 **J**ava**S**cript **O**bject **N**otation (JSON)

Om objecten op te slaan als strings in bijvoorbeeld localStorage, zouden we zelf een toString() methode kunnen schrijven. Het nadeel: dit zou een maintenance nightmare zijn aangezien men dit snel zou vergeten als we waarden toevoegen. We gaan dus gebruik maken van JSON.

Een object omzetten naar string met JSON:

```JavaScript
let student = {
  name: 'John',
  age: 30,
  isAdmin: false,
  courses: ['html', 'css', 'js'],
  wife: null
};
let json = JSON.stringify(student);
```

Een JSON string omzetten naar object:

```JavaScript
let user = JSON.parse(userDataStr);
```

> JSON is wel gevoelig voor subtiele typfouten, let dus goed op of gebruik een validator

## 13. **D**ocument **O**bject **M**odel (DOM)

Wat is DOM?

Vanuit een programma kan je een HTML document als volledig object benaderen.

- Bouwt een boomvoorstelling van het HTML document in het geheugen
- Biedt klassen en methodes (tree-gebaseerde API) aan om via code door de boom te navigeren en bewerkingen uit te voeren.

Een boom is opgebouwd uit verschillende nodes. Een node kan zijn:

- Document

Een **DOCUMENT_NODE** bevat de toegangspoort tot het DOM, het stelt het volledige document voor. Deze bevat een verwijzing naar het <html>-element.

- Element

Ieder html-element komt overeen met een **ELEMENT_NODE** in de boom

- Text

De tekst-inhoud van een element is een **TEXT_NODE**, voorgesteld als child van het element-node.

Om makkelijk elementen op te halen uit een HTML pagina, maken we gebruik van het `id` attribuut.

```JavaScript
const element = document.getElementById('productdetails');
```

### 13.1 JavaScript en de DOM (dynamisch updaten van de pagina)

Er zijn verschillende manieren om de DOM-tree te wijzigen, vertrekkend van een element:

- `insertAdjacentHTML(...,...)`
- `innerHTML(...)`
- `createElement(...)` + `setAttribute(...)` + `appendChild(...)`

- **`insertAdjacentHTML()`**

De functie `insertAdjacentHTML(position, text)` parset d meegeven HTML-tekst en voegt de resulterende nodes toe aan de DOM structuur op de meegegeven positie.

Posities:

```JavaScript
element.insertAdjacentHTML(position, text);
// Position moet 1 van de volgende waarden zijn:
// 'beforebegin' - voor het element
// 'afterbegin' - juist binnen het element, voor het eerste kindelement
// 'beforeend' - juist binnen het element, na het laatste kindelement
// 'afterend' - na het element (ev. closing bracket)
```

```HTML
<!-- beforebegin --->
<p>
  <!-- afterbegin-->
  foo
  <!-- beforeend-->
</p>
<!-- afterend -->
```

Voorbeeld:

```HTML
<p id="pId">Dit is de paragraaf</p>
```

```JavaScript
const element = document.getElementById('pId');
element.insertAdjacentHTML('afterbegin', '<div>Dit is de toegevoegde div</div>');
```

```HTML
<p id="pId"
><div>Dit is de toegevoegde div</div>
Dit is de paragraaf</p>
```

- **`innerHTML()`**

Via de `innerHTML`-property van een element kan je de HTML die zich binnen dat element bevindt opvragen/wijzigen. Merk op dat als je de innerHTML wijzigt, je alles die binnen het element aanwezig was overschrijft.

```JavaScript
const content = element.innerHTML;
element.innerHTML = htmlString;
```

Voorbeeld:

```HTML
<p id="pId">Dit is de paragraaf</p>
```

```JavaScript
const element = document.getElementById('pId');
element.innerHTML = '<div>Dit is een div!</div>';
```

```HTML
<p id="pId"><div>Dit is een div!</div></p>
```

### 13.2 Nodes

Je kan ook zelf expliciet nodes maken en toevoegen aan de DOM-tree.

### 13.2.1 Nodes bewerken

- Creatie van nodes

  - `const anElementNode = document.createElement(tagName)`
  - `const aTextNode = document.createTextNode(text)`

- Toevoegen van een node

  - `node.appendChild(newChild)`
    Voegt een node `newChild` toe na de laatste child-node van `node`. De nieuwe toegevoegde node wordt geretourneerd.

```JavaScript
const divElement = document.createElement("div");
divElement.setAttribute("id", "divId");
const divTekst = document.createTextNode("Hier is de tekst voor de div...");
divElement.appendChild(divTekst);
element.appendChild(divElement);
```

- Verwijderen van een node

  - `removeChild(removeChild)`
    Verwijdert een child node van de document tree. De verwijderde node wordt geretourneerd (en kan dus eventueel nog verder gebruikt worden)

- Vervangen van een node

  - `replaceChild(newChild, oldChild)`
    Vervangt de _oldChild_ node voor de _newChild_ node. De verwijderde oldchild node wordt geretourneerd (en kan dus eventueel nog verder gebruikt worden).

- Clonen van een node
  - `cloneNode(deepcopy)`
    Creëert en retourneert een exacte kloon. Als de boolean parameter _deepCopy_ gelijk is aan true wordt een kloon gemaakt van de node zelf en de volledige subtree, anders wordt enkel een kloon gemaakt van de node zelf.

### 13.2.2 Node attributen bewerken

- `setAttribute(attrName, attrValue)`

Wordt gebruikt om een attribuut in te stellen. Voorbeeld:

```JavaScript
const divElement = document.createElement("div");
divElement.setAttribute("id", "divId");
```

- `getAttribute(attrName)`

Het attribuut van een node verkrijgen.

- `removeAttribute(attrName)`

Een attribuut van een node verwijderen.

### 13.3 Flexibel nodes selecteren

- `getElementById(id)`

  - geeft het eerste element met de opgegeven _id_
  - de zoekbewerking start meestal vanaf het document element, maar je kan evengoed van elk ander element starten

- `getElementsByTagName(tagname)`

  - retourneert een **live HTML collection** met alle elementen (0 of meer) met de opgegeven _tagname_
  - een HTML collection is een array-like object van elementen en voorziet properties en functies om elementen te selecteren in de lijst

- `getElementsByClassName(value)`

  - retourneert een **live HTML collection** met alle elementen met d e opgegeven _value_ als waarde voor het class attribuut

- `querySelector(CSS selector)`

  - retourneert het eerste element dat voldoet aan de opgegeven CSS selector

- `querySelectorAll(CSS selector)`
  - retourneert een **non live (static)** nodelist met alle elementen die voldoen aan de opgegeven CSS selector

### 13.4 DOM Cheatsheet

Klik [hier](https://christianheilmann.com/stuff/JavaScript-DOM-Cheatsheet.pdf) om de DOM Cheatsheet te bekijken (gemaakt door Christian Heilmann).

## 14. Asynchroon programmeren (callback & promises)

Vooraleer we asynchroon programmeren, moeten we eerst weten wat synchroon programmeren betekent.

In de echte kern is JavaScript een synchrone taal. Dit wil kortweg zeggen dat JavaScript maar 1 taak tegelijkertijd kan uitvoeren.

### 14.1 Asynchroon

Stel, we voeren een methode uit die een waarde teruggeeft. De methode duurt 10 seconden om te verwerken.

```JavaScript
let notAMoon = buildADeathStarAsync();
```

Daaronder hebben we een methode staan die de waarde van `notAMoon` nodig heeft.

```JavaScript
let alderaan = destroyPlanet(notAMoon);
```

JavaScript zal niet wachten tot de methode `buildDeathStarAsync()` is uitgevoerd, wat dus zal leiden tot een `TypeError` (`destroyPlanet` zal deze error gooien omdat notAMoon undefined is). Om dit te voorkomen hebben wij callback methodes en promises.

### 14.2 Callback functies

Callback functies bieden een oplossing voor dit probleem. We willen namelijk niet wachten op het resultaat van een functie om andere functies te starten, die geen dependency hebben met de eerste functie.

In plaats van het result te retourneren en dit result te gebruiken door een andere functie, gaan we de andere functie (callback functie) als parameter meegeven aan de lang durende functie. In de langdurende functie kunnen we dan de callback functie aanroepen.

Voorbeeld:

```JavaScript
function buildDeathStarAsync(callbackParameter){
  //do a lot of stuff, it takes time to build a death star (10sec)
  setTimeout(function(){
    const planet = {name: 'Alderaan', moon:false}
    console.log(`Builded ${planet.name}, it took 10 seconds`);
    callbackParameter(planet); //Hier wordt de callback aangeroepen, nadat al de rest gedaan is.
  },10000);
}
function destroyPlanet(planet){
  //do a lot of stuff, it takes time to destroy a death star (2sec)
  setTimeout(function(){
    console.log(`Destroyed ${planet.name}, it took 2 seconds`);
    console.log(planet.name === 'Alderaan'?'Aaaaaaargh, Alderaan destroyed\n'.repeat(10):'Nothing seriously happened’)
  },2000);
}

buildDeathStarAsync(destroyPlanet);
```

Callback functies bieden dus een oplossing voor het probleem van asynchroon programmeren. Ze worden vaak gekoppeld aan eventhandlers (click, load, keyup,...) omdat je niet weet wanneer en hoe lang het event zal plaatsvinden.

Een callback functie kan op verschillende manieren gedeclareerd worden:

- `function nameFunction(par) { ... }`
- `const nameFunction = function(par) {...}`
- Anonymous function: `function(par) {...}`
- Arrow notation: `(par) => {...}`

### 14.2.1 Callback (addEventListener)

```JavaScript
elText = document.getElementById("textButtons");

const btn = document.getElementById('button');
const btn1 = document.getElementById('button');

function clickMe(event){
  showText(event);
}

function showText(evt){
  elText.innerHTML =
  `You clicked on button:
  ${evt.target.innerHTML}`
}

btn.addEventListener('click', (event) => { showText(event); });
btn1.addEventListener('click', clickMe);
```

> **(!)** Callback hell: Callbacks werken prima zolang het kleine geïsoleerde functies zijn. Van zodra de callback zelf callbacks heeft en deze dan nog ook eens een callback, enzovoort, enzoverder, dan krijgen we zogenaamde 'callback hell'. Dit is allesbehalve overzichtelijk en leidt bijna zeker tot fouten.

### 14.3 Promise

Het idee achter promises is het resultaat van een asynchrone operatie bij te houden in een variabele en deze te gaan gebruiken waar en wanneer je wilt.

```JavaScript
let deathStarPromise = buildADeathStarAsync();
let army = buildCloneArmyAsync();
```

De asynchrone operatie `buildADeathStarAsync()` wordt toegekend aan `deathStarPromise`.

Je kan reageren met het toekomstige resultaat van de eerste asynchrone functie door gebruik te maken van een `then` method, die een callback bevat als parameter, van de promise. Deze callback wordt uitgevoerd van zodra `buildADeathStarAsync` succesvol is afgehandeld.

Indien de `buildADeathStarAsync` niet succesvol is afgehandeld, kan men via de catch method van de promise dit ook gaan afhandelen via een callback.

Duidelijker voorbeeld:

```JavaScript
const myPromise = new Promise((resolve, reject) => {
  let a = 1 + 2;
  if(a == 2) {
    resolve('Succes!');
  } else {
    reject('Failed!');
  }
});

myPromise.then((resolve) => {...}, (reject) => {...});
```

In zowel `resolve()` als `reject()` kan men alles doorgeven wat je wilt (dit kunnen meerdere parameters zijn).

Onderstaande code is hetzelfde als hierboven, maar dan met `.catch()` uitgewerkt.

```JavaScript
const myPromise = new Promise((resolve, reject) => {
  let a = 1 + 2;
  if(a == 2) {
    resolve('Succes!');
  } else {
    reject('Failed!');
  }
});

myPromise
  .then((resolve) => {...})
  .catch((reject) => {...});
```

> Promises kunnen zich in 3 toestanden bevinden:
>
> - Pending: Het resultaat van de promise is nog niet bepaald
> - Fulfilled: De asynchrone operatie is afgerond en de promise heeft een waarde.
> - Rejected: De asynchrone operatie is niet goed afgerond waardoor de promise niet gerealiseerd kan worden.
>
> Wanneer de toestand 'pending' is, kan deze overgaan in fulfilled of rejected. Is deze al fulfilled of rejected, dan kan deze niet meer veranderen.

### 14.3.1 Promise (met extra argumenten)

Stel, we willen argumenten meegeven aan een Promise. Dit kan niet zomaar, maar, we kunnen deze wel in een functie stoppen en de `new Promise()` returnen. Voorbeeld:

```JavaScript
const myFunction = (username, password) => {
  return new Promise((resolve, reject) => {
    //Stuff using username & password
    if(/*Everything went fine*/) {
      resolve('It worked!');
    } else {
      reject('Failed :(');
    }
  });
}
```

We kunnen dan de functie als volgt aanroepen:

```JavaScript
myFunction(username, password)
  .then((resolve) => {...})
  .catch((reject) => {...});
```

### 14.3.2 `Promise.all` en `Promise.race`

Het probleem met callbacks was: een functie pas uitvoeren nadat verschillende andere callbacks uitgevoerd waren.

#### 14.3.2.1 `Promise.all`

`Promise.all` is een statische functie die net dat bereikt: je geeft er een array van promises aan mee, en hij wodt geresolved met een array van values als ze allemaal afgerond zijn (je krijgt dus een array met alle values).

> **Belangrijk**: Als er 1 van de promises faalt, dan faalt de volledige `Promise.all`.

Voorbeeld:

```JavaScript
const gok1 = () =>
  new Promise((resolve, reject) => {
    const gok = Number.parseInt(prompt("Geef een getal tussen 1 en 3"));
    // const randomWaarde = Math.floor(Math.random() * 3) + 1;
    const randomWaarde = 2;
    gok === randomWaarde ? resolve("Haardroger") : reject("Geen haardroger");
  });
const gok2 = () =>
  new Promise((resolve, reject) => {
    const gok = Number.parseInt(prompt("Geef een getal tussen 1 en 5"));
    // const randomWaarde = Math.floor(Math.random() * 5) + 1;
    const randomWaarde = 2;
    gok === randomWaarde ? resolve("Koelkast") : reject("Geen koelkast");
  });
const gok3 = () =>
  new Promise((resolve, reject) => {
    const gok = Number.parseInt(prompt("Geef een getal tussen 1 en 8"));
    // const randomWaarde = Math.floor(Math.random() * 8) + 1;
    const randomWaarde = 2;
    gok === randomWaarde ? resolve("Vliegreis") : reject("Geen vliegreis");
  });

function init() {
  document.getElementById("gokMaar").onclick = () => {
    Promise.all([gok1(), gok2(), gok3()]).then(values => {
      console.log(values);
    }).catch(values => {
      console.log(values);
    });
  }
}
window.onload = init;
```

Resultaat:

```JavaScript
// Als enkel gok2 fout is => catch
Geen koelkast
// Als geen enkele gok fout is => then
(3) ['Haardroger', 'Koelkast', 'Vliegreis']
// Als enkel gok3 fout is => catch + fail fast
Geen vliegreis
// Als gok1, gok2 en gok3 fout zijn => catch + fail fast
Geen haardroger
```

Kortweg: als er meerdere waarden fout zijn zal deze enkel de eerste foute waarden printen (fail fast).

#### 14.3.2.1 `Promise.race`

`Promise.race` is gelijkaardig aan `Promise.all`, maar eigenlijk het tegenovergestelde.

Bij `Promise.all` stopt de promise als er 1 rejected is, bij `Promise.race` stop de promise als er 1 resolved is, maar ook als er 1 rejected is.

---

> Extra info (beperkingen van Promise):
>
> - Promises maken het werken met asynchrone code een stuk aangenamer, perfect zijn ze natuurlijk niet.
> - Een eerste probleem is dat een promise altijd start, en altijd afgerond wordt, dus ook als er nooit iemand `.then()` aanroept, of als het resultaat je niet langer interesseert kan je een promise niet 'cancelen'.
> - Eenmaal een promise afgerond is, kan je ze ook niet makkelijk opnieuw uitvoeren, de promise zelf bevat enkel het resultaat.

## 15. AJAX - fetch API

**A**synchronous **J**avaScript **A**nd **X**ML (AJAX) is een term voor het ontwerp van interactieve webpagina's waarin asynchroon gevraagde gegevens worden opgehaald van de webserver. Daardoor hoeven dergelijke pagina's in hun geheel ververst te worden.

### 15.1 Een eenvoudig voorbeeld

Om AJAX requests illustreren hebben we een server nodig waar we data kunnen opvragen. We maken gebruik van de [joke API](https://official-joke-api.appspot.com/random_joke).

We schrijven een `ajaxRequest` methode:

```JavaScript
function ajaxRequest(url){
	// creatie van het XHR object
	const request = new XMLHttpRequest();
	// open(Methode, URL, Asynchronous, Username, Password)
	request.open('GET', url);
	// callback functie declareren om de request af te handelen
	request.onreadystatechange = () => {
		// readyState en status worden geëvalueerd
		if (request.readyState === 4 && request.status === 200) {
			console.log(request.responseText);
		}
	};
	// verstuur het verzoek naar de server
	request.send();
}

class JokeApp{
	getData(){
		ajaxRequest('https://official-joke-api.appspot.com/random_joke');
	}
}

const init = function(){
	const jokeApp = new JokeApp();
	document.getElementById("joke").onclick = () => {
		jokeApp.getData();
	};
}

window.onload = init;
```

Uitleg:

- Om te beginnen maken we een `XMLHttpRequest()` object aan.

- `open` method

  - `open(method, url, asynchronous, userName, password)`
    - `method` HTTP request method: GET - POST - HEADER - PUT - DELETE
    - `url` De URL waar het request naar verstuurd wordt (het adres). Dit kan ook een tekst, json, xml bestand zijn.
    - `asynchronous` boolean die aangeeft of het request al dan niet asynchroon is. Niet verplicht - default true.
    - `userName` & `password` voor eventuele authenticatie. Beide zijn niet verplicht.

- `send` method

  - verstuurt het request naar de server
  - data kunnen als parameter naar de server gestuurd worden

- Properties van het XHR object:

  - `readyState` bevat de status van het object

    - `0` - `UNSENT` (client has been created, `open()` not called yet)
    - `1` - `OPENED` (`open()` has been called)
    - `2` - `HEADERS_RECEIVED` (`send()` has been called and the headers and status are available)
    - `3` - `LOADING` (Downloading, `responseText` holds partial data)
    - `4` - `DONE` (the operation is complete)

  - `status` geeft de http status die door de server is teruggegeven

    - 200: OK
    - 404: Page not found
    - ...

  - `onreadystatechange`
    - koppelt een callback functie
    - deze wordt uitgevoerd elke keer als de `readyState` van waarde wijzigt
  - `responseText` is de data dat de server als string teruggeeft (kan ook JSON string zijn)
  - `reponseXML` is de data die de server teruggeeft als XML

> Heel vaak wordt er een JSON response gegeven. Deze wordt wel als string gedownload, dus vaak moeten we deze nog parsen. Dit kunnen we doen met `const joke = JSON.parse(request.reponseText);`.

### 15.2 AJAX en promises

In plaats van het verwerken van het Ajax request te koppelen aan een callback functie, maken we gebruik van een promise. Voorbeeld:

```JavaScript
function ajaxRequest(url){
	return new Promise((resolve, reject) => {
		const request = new XMLHttpRequest();
		request.open('GET',url );
		request.onreadystatechange = () => {
			if (request.readyState === 4){
				if (request.status === 200) {
					resolve(JSON.parse(request.responseText));
				}
				else {
					reject(`ERROR ${request.status} while processing.`);
				}
			}
		}
		request.send();
	});
}
```

We zien nu dat we de Promise in de return stoppen van een functie (`ajaxRequest`). Zo kunnen we makkelijk parameters doorgeven aan een Promise. Als de `readyState` 4 is en de `status` 200, dan kunnen we de promise resolven. In de resolve geven we het antwoord mee.

Als de `readyState` 4 is, maar het antwoord is **niet** 200, dan wil dit zeggen dat er iets fout is gegaan. Dan rejecten we de promise met de error als argument.

We kunnen dan makkelijk de request verder afhandelen:

```JavaScript
class JokeApp{
	getData(){
		ajaxRequest('https://official-joke-api.appspot.com/random_joke')
		.then(resolveValue => { this.toHtml(resolveValue); })
		.catch(rejectValue => { console.log(rejectValue); });
	}
	toHtml(joke) {
		document.getElementById("category").innerHTML = `Category = ${joke.type}`;
		document.getElementById("setup").innerHTML = `Q: ${joke.setup}`;
		document.getElementById("punchline").innerHTML = `A: ${joke.punchline}`;
	}
}
```

### 15.3 Fetch API

Om een AJAX request uit te voeren moet er steeds dezelfde code gebruikt worden. Om dit op en meer gestructureerde manier en compacter te doen is de [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) ontwikkeld.

De Fetch API is vergelijkbaar met de werking van XHR.

- de `fetch()` methode heeft één verplicht argument, het 'path' (vaak url) naar de 'resource' die je wil ophalen.
- Deze methode retourneert een Promise die het antwoord zal verwerken van het 'request', of dit succesvol is of niet.
- Eenmaal het antwoord is ontvangen, zijn er een aantal mogelijkheden om het antwoord (body) te verwerken:
  - `Body.json()`: retourneert een Promise dat de body parsed naar JSON
  - `Body.text()`: retourneert een Promise dat de body parsed naar text

Het grote blok code dat we hierboven bekeken hebben wordt dat verkleind tot:

```JavaScript
function fetchRequest(url) {
	return fetch(url)
		.then(body => body.json());
}

class JokeApp {
	getData() {
		fetchRequest('https://official-joke-api.appspot.com/random_joke') //retourneert promise object met response
			.then(data => this.toHtml(data)) //resolve promise (argument is response)
			.catch(error => console.error(error)); //reject promise (argument is error)
	}
	toHtml(joke) {
		document.getElementById("category").innerHTML = `Category = ${joke.type}`;
		document.getElementById("setup").innerHTML = `Q: ${joke.setup}`;
		document.getElementById("punchline").innerHTML = `A: ${joke.punchline}`;
	}
}
```

### 15.3.1 Fetch Request status

Als we een fetch request versturen, kan het ook zijn dat de API niet bereikbaar is (we krijgen dus een 404 weer).

Aangezien onze fetch request een promise is, zou je denken dat we dit kunnen opvangen met catch. Dit is **niet** het geval! Je moet eerst kijken of het resultaat van de fetch 'ok' is. Voorbeeld:

```JavaScript
fetch('example.com/api')
  .then(res => {
    if(res.ok) {
      //SUCCES
      return res.json()
    } else {
      //ERROR
    }
  }).then(data => console.log(data));
```

### Tips & tricks (dingen die ik zelf vaak vergeet)

- Tekstveld uitlezen: `document.getElementById('test').value`
- Element src bewerken: `document.getElementById('test').src = 'img/test.png'`
- String individuele character: `string.charAt(0)`
- Om iets in een string te zoeken, gebruiken we `str.includes()`
- Willekeurig getal genereren: `Math.floor(Math.random() * 10) + 1` (tussen 1 en 10)
- Enhanced for bij Arrays:

```JavaScript
for(let element of fruit) {
  console.log(element);
}
```

- String naar array: `str.split('');` of `[...str]`
- String naar int: `parseInt(str)`
