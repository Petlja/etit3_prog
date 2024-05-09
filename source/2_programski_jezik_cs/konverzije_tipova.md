# Конверзије типова

Програмски језик C# могуће је вршити конверзије између било која два нумеричка
типа - имплицитне или експлицитне. Експлицитне конверзије врше се каст изразима
(енгл. *Cast Expression*) облика `(T)E`, где је `E` израз, а `T` жељени тип. На
пример:

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
| `decimal` | `sbyte`, `byte`, short, ushort, int, uint, long, ulong, float, double, nint, or nuint
| `nint`    | `sbyte`, `byte`, short, ushort, int, uint, ulong, or nuint
| `nuint`   | `sbyte`, `byte`, short, ushort, int, uint, long, or nint


