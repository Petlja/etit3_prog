# Стрингови

Стрингови у програмским језицима C и C# представљају текстуалне податке и
омогућавају манипулацију текстом, али се значајно разликују. У програмском
језику C, стрингови су низови карактера који се завршавају карактером `\0`, где
нема уграђене подршке за стрингове као објекте са методама - све операције
извршавају се преко функција из библиотеке `<string.h>`.

Једна од важних карактеристика стрингова за програмере који развијају
апликације које нису на енглеском језику је да објекти типа стринг подржавају
UNICODE, што значи да могу представљати текст у било ком писму или језику.

У програмском језику C#, стрингови су објекти класе `System.String`. То значи
да стрингови имају много уграђених метода за манипулацију текстом. Декларација
и иницијализација стринга је једноставна:

```cs
string pozdrav = "Hello, World!";
```

Након декларације и иницијализације, доступне су многе методе и својства за рад
са стринговима, као што су `Length`, `Substring`, `IndexOf`, `Replace`,
`ToUpper`, `ToLower`, итд. На пример:

```cs
string pozdrav = "Hello, World!";
int duzina = pozdrav.Length;          // 13 - дужина стринга
string velika = pozdrav.ToUpper();    // HELLO, WORLD!
string sub = pozdrav.Substring(7, 5); // World
```

Програмски језик C# подржава интерполацију стринга која омогућава лакше
убацивање променљивих у стрингове. На пример:

```cs
int god = 17;
string ime = "Velimir";
string poruka = $"{ime} je napunio {god} godina";
```

У програмском језику C#, стрингови су имутабилни, што значи да након што се
креирају, не могу бити промењени. Свака промена на стрингу ствара нови објекат
типа стринг. У програмском језику C, стринг може бити модификован директно.

```cs
string original = "Hello";
string promenjen = original.Replace('H', 'J');  // Нови стринг "Jello"
```

Конкатенацију стрингова можеш вршити коришћењем оператора `+` или метода као
што је `String.Concat`.

```cs
string str1 = "Hello";
string str2 = "World";
string rezultat = str1 + ", " + str2 + "!";  // "Hello, World!"
```

Као што је већ написано, објекат типа стринг има много уграђених метода и
својстава за манипулацију са текстом. Све методе и својства наведене су у
званичној [документацији](https://learn.microsoft.com/en-us/dotnet/api/system.string?view=netframework-4.8).
Примери употребе неких метода за рад са стринговима:

```cs
string text = "Hello, World!";
string sub = text.Substring(7, 5);             // World
int indeks = text.IndexOf('W');                // 7
string zamenjen = text.Replace("World", "C#"); // Hello, C#!
string velika = text.ToUpper();                // HELLO, WORLD!
string[] reci = text.Split(' ');               // reci[0] = Hello, reci[1] = World!
string spojeni = string.Join(" ", reci);       // Hello, World!
```

`String.Format` омогућава форматирање стрингова у шаблоне. На пример:

```cs
string formatiran = string.Format("Ime: {0}, Godine: {1}", ime, godine);
```

`ToString()` методе многих типова подржавају форматирање. На пример:

```cs
DateTime trenutno = DateTime.Now;
string datumVreme = trenutno.ToString("dd-MM-yyyy HH:mm:ss");
```

Стринг литерали могу садржати прелазне секвенце као што су `\n` (нова линија),
`\t` (таб), итд. Списак свих прелазних секвенци дат је у
[прилогу](../7_dodaci/prelazne_sekvence.md). Вербатим стринг литерали (почињу
са `@`) омогућавају лакше коришћење путања и текста са специјалним знаковима.
На пример:

```cs
string putanja = @"C:\Users\Velimir\Documents";
string linije = @"prva
druga
treca";
```

Поређење стрингова можеш вршити методама као што су `Equals`, `Compare` и
`CompareOrdinal`. На пример:

```cs
bool poredi = string.Equals("Hello", "HELLO"); // False
bool poredi = string.Equals("hello", "HELLO", StringComparison.OrdinalIgnoreCase); // True
int poredi = string.Compare("Hello", "HELLO"); // -1
```
