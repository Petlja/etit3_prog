# Конверзије типова

О [експлицитним и имплицитним конверзијама типова](https://petlja.org/sr-Latn-RS/kurs/11231/4/8010)
у програмском језику C учио си у првом разреду.
У програмском језику C# могуће је вршити конверзије између било која два
нумеричка типа - имплицитно или експлицитно. Експлицитне конверзије врше се
каст изразима (енгл. *Cast Expression*) облика `(T)E`, где је `E` израз, а `T`
жељени тип. На пример:

```cs
double x = 12.345;
int y = (int)x;
Console.WriteLine(y);    // 12
```

## Имплицитне конверзије

У следећој табели приказане су све предефинисане имплицитне конверзије између
нумеричких типова:

| из       | у                                                                                                   |
|----------|-----------------------------------------------------------------------------------------------------|
| `sbyte`  | `short`, `int`, `long`, `float`, `double`, `decimal` или `nint`                                     |
| `byte`   | `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double`, `decimal`, `nint` или `nuint` |
| `short`  | `int`, `long`, `float`, `double`, `decimal` или `nint`                                              |
| `ushort` | `int`, `uint`, `long`, `ulong`, `float`, `double`, `decimal`, `nint` или `nuint`                    |
| `int`    | `long`, `float`, `double`, `decimal` или `nint`                                                     |
| `uint`   | `long`, `ulong`, `float`, `double`, `decimal` или `nuint`                                           |
| `long`   | `float`, `double` или `decimal`                                                                     |
| `ulong`  | `float`, `double` или `decimal`                                                                     |
| `float`  | `double`                                                                                            |
| `nint`   | `long`, `float`, `double` или `decimal`                                                             |
| `nuint`  | `ulong`, `float`, `double` или `decimal`                                                            |

Ако се у програму врше имплицитне конверзије, онда требаш водити рачуна о
губитку прецизности. Имплицитне конверзије из типова `int`, `uint`, `long`,
`ulong`, `nint` или `nuint` у тип `float`, односно из типова `long`, `ulong`,
`nint` или `nuint` у тип `double` могу да доведу до губитка прецизности, али не
и до губитка реда величине. На пример:

```cs
int x = 1234554321;
float y = x;
Console.WriteLine(y);    // 1.234554E+09
```

Остале имплицитне конверзије не могу да доведу до губитка прецизности.

У програмском језику C# нису дефинисане имплицитне конверзије у типове `byte` и
`sbyte`, као ни имплицитне конверзије из типова `double` и `decimal`. Нису
дефинисане ни имплицитне конверзије између типа `decimal` и типова `float` и
`double`.

## Експлицитне конверзије

У следећој табели приказане су све предефинисане експлицитне конверзије између
нумеричких типова, за које нису дефинисане имплицитне конверзије:

| из        | у                                                                                                          |
|-----------|------------------------------------------------------------------------------------------------------------|
| `sbyte`   | `byte`, `ushort`, `uint`, `ulong` или `nuint`                                                              |
| `byte`    | `sbyte`                                                                                                    |
| `short`   | `sbyte`, `byte`, `ushort`, `uint`, `ulong` или `nuint`                                                     |
| `ushort`  | `sbyte`, `byte` или `short`                                                                                |
| `int`     | `sbyte`, `byte`, `short`, `ushort`, `uint`, `ulong` или `nuint`                                            |
| `uint`    | `sbyte`, `byte`, `short`, `ushort`, `int` или `nint`                                                       |
| `long`    | `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `ulong`, `nint` или `nuint`                             |
| `ulong`   | `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `nint` или `nuint`                              |
| `float`   | `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `decimal`, `nint` или `nuint`          |
| `double`  | `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `decimal`, `nint` или `nuint` |
| `decimal` | `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double`, `nint` или `nuint`  |
| `nint`    | `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `ulong` или `nuint`                                     |
| `nuint`   | `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long` или `nint`                                       |

Експлицитне конверзије могу да доведу до губитка података или грешака
"преливања", ако тип који се конвертује (изворни тип) није у опсегу типа у који
се конвертује (одредишни тип). Ако је изворни тип већи од одредишног, онда се
изворна вредност скраћује одбацивањем битова. На пример:

```cs
using System;

internal class Program
{
    static void Main()
    {
        int veca = 300;
        byte manja = (byte)veca;
        Console.WriteLine("Originalna vrednost: " + veca);
        Console.WriteLine("Konvertovana vrednost: " + manja);
    }
}
```

Извршавањем овог програма у конзоли ће се исписати:

```text
Originalna vrednost: 300
Konvertovana vrednost: 44
```

Ако је изворни тип мањи од одредишног, онда се изворна вредност проширује или
знаком или нулама, тако да одговара величини одредишног типа.

```cs
using System;

internal class Program
{
    static void Main()
    {
        sbyte manja = -30;
        int veca = (byte)manja;
        Console.WriteLine("Originalna vrednost: " + manja);
        Console.WriteLine("Konvertovana vrednost: " + veca);
    }
}
```

Извршавањем овог програма у конзоли ће се исписати:

```text
Originalna vrednost: -30
Konvertovana vrednost: 226
```

Ако је изворни тип исте величине као и одредишни, онда се изворна вредност
третира као одредишна вредност.

Ако се тип `decimal` конвертује у неки целобројни тип, изворна вредност се
заокружује. Ако је заокружена изворна вредност ван опсега одредишне вредности,
долази до грешке "преливања". Ако се типови `float` или `double` конвертују у
неки целобројни тип, изворна вредност се такође заокружује. Ако је заокружена
изворна вредност ван опсега одредишне вредности, долази до грешке ""преливања" или
је резултат неодређена вредност типа одредишта.

Ако се тип `double` конвертује у тип `float`, изворна вредност се заокружује на
најближу одредишну вредност. Ако је изворна вредност премала или превелика да
стане у одредишну, резултат је нула или бесконачно. Ако се типови `float` или
`double` конвертују у тип `decimal`, изворна вредност се конвертује у одредишну
и заокружује на најближи број до двадесетосме децимале. Ако је изворна вредност
премала, онда је резултат нула, односно, ако је изворна вредност превелика
долази до грешке "преливања". На крају, ако се тип `decimal` конвертује у типове
`float` или `double`, изворна вредност се заокружује на најближу одредишну
вредност.
