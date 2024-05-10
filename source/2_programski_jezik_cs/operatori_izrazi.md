# Оператори и изрази

Операторе можеш да примењујеш над подацима различитих уграђених типова.
Оператори се могу поделити у више група:

* аритметички оператори,
* релацијски оператори (оператори поређења и једнакости),
* логички оператори (Буловски) и
* битски оператори.

Ови оператори се могу преоптеретити ако се примењују над кориснички-дефинисаним
типовима података.

Најједноставнији C# изрази су литерали (нпр. цело или реалан број) и имена
променљивих. Њих можеш комбиновати у сложене изразе користећи операторе.
Приоритет и асоцијативност оператора одређују редослед којим се извршавају
операције у изразу. Тај редослед, наметнут приоритетом оператора и
асоцијативношћу, можеш да промениш заградама.

## Аритметички оператори

Као и у програмском језику C, аритметички оператори у програмском језику C#
могу бити:

* унарни: инкремент `++`, декремент `--`, плус `+` и минус `-` и
* бинарни: множење `*`, дељење `/`, остатак `%`, сабирање `+` и одузимање `-`.

Њих можеш да користиш над операндима целобројног типа или типова са покретном
тачком. У случају целобројних типова, бинарни оператори и унарни плус и минус
дефинисани су за типове `int`, `uint`, `long` и `ulong`. Ако су операнди типа
`sbyte`, `byte`, `short`, `ushort` или `char`, њихове вредности се прво
конвертују у `int` па се онда извршава операција која даје резултат типа `int`.

У следећим програмима демонстрирана је примена оператора инкрементирања и
декрементирања...

```cs
int a = 1;
double b = 1.5;

// Postfiksni inrekement operatori
Console.WriteLine(a++);    // 1
Console.WriteLine(b++);    // 1.5
Console.WriteLine(a);      // 2
Console.WriteLine(b);      // 2.5

// Prefiksni inkrement operatori
Console.WriteLine(++a);    // 3
Console.WriteLine(++b);    // 3.5
Console.WriteLine(a);      // 3
Console.WriteLine(b);      // 3.5

// Postfiksni derekement operatori
Console.WriteLine(a--);    // 3
Console.WriteLine(b--);    // 3.5
Console.WriteLine(a);      // 2
Console.WriteLine(b);      // 2.5

// Prefiksni dekrement operatori
Console.WriteLine(--a);    // 1
Console.WriteLine(--b);    // 1.5
Console.WriteLine(a);      // 1
Console.WriteLine(b);      // 1.5
```

...примена унарних плус и минус оператора...

```cs
int a = 1;
Console.WriteLine(+a);     // 1
Console.WriteLine(a);      // 1
Console.WriteLine(-a);     // -1
Console.WriteLine(a);      // 1
```

...примена оператора множења, дељења, остатка, сабирања и одузимања

```cs
int a = 5, b = 2;
double c = 5.5, d = 2.2;
Console.WriteLine(a * b);     // 10
Console.WriteLine(c * d);     // 12.1
Console.WriteLine(a / b);     // 2
Console.WriteLine(c / d);     // 2.5
Console.WriteLine(a % b);     // 1
Console.WriteLine(c % d);     // 1.1
Console.WriteLine(a + b);     // 7
Console.WriteLine(c + d);     // 7.7
Console.WriteLine(a - b);     // 3
Console.WriteLine(c - d);     // 3.3
```
